# Runbook: Database Connection Pool Exhaustion

## Symptoms
- 5xx error rate spike on API endpoints
- "Timeout acquiring connection from pool" errors in API logs
- Active DB connections at or near max limit
- Request latency p99 > 5 seconds

## Immediate Mitigation

1. **Check current pool status**
   ```sql
   SELECT count(*) FROM pg_stat_activity WHERE state = 'active';
   SELECT count(*) FROM pg_stat_activity WHERE state = 'idle';
   ```

2. **Increase pool size** (if below 80% of server max_connections)
   - Edit `postgresql.conf` or use `ALTER SYSTEM SET`
   - Reload config: `SELECT pg_reload_conf();`
   - No restart required for pool size increase
   - Recommended: increase to 2x current limit

3. **Kill long-running queries** (if holding connections)
   ```sql
   SELECT pid, now() - pg_stat_activity.query_start AS duration, query
   FROM pg_stat_activity
   WHERE state != 'idle' AND now() - pg_stat_activity.query_start > interval '5 minutes';
   ```
   - Use `SELECT pg_terminate_backend(pid);` to kill specific queries
   - WARNING: may cause data inconsistency if mid-transaction

4. **Verify fix** — confirm 5xx rate drops below 1% within 5 minutes

## Post-Mitigation

5. **Monitor** — watch connection count for 30 minutes, ensure it stabilises below 80% of new limit
6. **Enable alerts** — set threshold at 80% of max_connections
7. **Review traffic source** — identify what caused the spike

## Prevention

- Set connection pool alerts at 80% utilisation
- Implement connection pool auto-scaling
- Coordinate with Marketing/Product on campaigns expected to drive traffic spikes
- Consider read replicas for read-heavy traffic
