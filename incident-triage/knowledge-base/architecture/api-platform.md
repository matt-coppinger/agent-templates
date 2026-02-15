# API Platform Architecture

## Overview
- **API Gateway**: Nginx-based, 3 instances behind AWS ALB
- **Primary cluster**: 6 application servers (Node.js)
- **Database**: PostgreSQL 15 (primary + 2 read replicas)
- **Cache**: Redis cluster (3 nodes)
- **CDN**: CloudFront for static assets

## Database Configuration
- **Primary**: db-primary.internal (m5.2xlarge)
- **Read replicas**: db-replica-1.internal, db-replica-2.internal
- **Connection pool**: max_connections = 100 per application server
- **Total max**: 600 connections across all app servers
- **Server max_connections**: 1000

## Traffic Patterns
- Normal peak: ~5,000 req/sec (weekdays 10:00-16:00 UTC)
- Marketing campaigns: typically 2-3x normal traffic
- Black Friday: up to 5x normal traffic (pre-scaled)

## Monitoring
- **APM**: Datadog (error rates, latency, throughput)
- **Database**: PostgreSQL native metrics + Datadog integration
- **Alerts**: PagerDuty integration via Datadog
- **Dashboards**: Grafana for infrastructure, Datadog for application

## SLAs
- API uptime: 99.9% (43 min downtime/month)
- API latency p99: < 500ms
- Error rate: < 0.5%
