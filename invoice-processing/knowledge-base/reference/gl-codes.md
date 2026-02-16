# General Ledger Code Reference

## Expense Accounts (6000–6999)

| Code | Account Name | Description | Default VAT |
|------|-------------|-------------|-------------|
| 6100 | Travel | Rail, air, taxi, mileage | Standard |
| 6110 | Accommodation | Hotels, serviced apartments | Standard |
| 6120 | Meals & Entertainment | Client entertainment, team meals | Standard |
| 6200 | Office Supplies | Stationery, printer consumables, sundries | Standard |
| 6210 | Telecommunications | Phone, broadband, mobile | Standard |
| 6220 | Utilities | Electricity, gas, water | Standard (5% for domestic) |
| 6300 | Software Licences | SaaS subscriptions, licence fees | Standard/Reverse charge |
| 6310 | Cloud Services | AWS, Azure, hosting | Standard/Reverse charge |
| 6400 | Professional Services | Legal, audit, consultancy | Standard |
| 6410 | Recruitment Fees | Agency fees, job advertising | Standard |
| 6500 | Marketing | Advertising, events, sponsorship | Standard |
| 6510 | Subscriptions | Trade publications, memberships | Standard/Exempt |
| 6600 | Training | Courses, conferences, materials | Standard |
| 6700 | Insurance | Business insurance premiums | Exempt |
| 6800 | Bank Charges | Transaction fees, FX charges | Exempt |
| 6900 | Miscellaneous | Sundry expenses not elsewhere classified | Standard |

## Capital Accounts (7000–7999)

| Code | Account Name | Description | Default VAT |
|------|-------------|-------------|-------------|
| 7100 | Equipment | IT hardware, office equipment | Standard |
| 7200 | Furniture | Desks, chairs, fixtures | Standard |
| 7300 | Vehicles | Company vehicles | Standard |
| 7400 | Leasehold Improvements | Office fit-out, renovations | Standard |

## Balance Sheet Accounts (Referenced in Journal Entries)

| Code | Account Name | Description |
|------|-------------|-------------|
| 2100 | Accounts Payable | Trade creditors control account |
| 2101 | Accruals | Accrued expenses |
| 2200 | VAT Output | VAT collected on sales |
| 2201 | VAT Input | VAT recoverable on purchases |
| 1200 | Bank Account | Main operating account |

## Cost Centres

| Code | Department |
|------|-----------|
| EXEC | Executive |
| FIN | Finance |
| HR | Human Resources |
| IT | Information Technology |
| MKT | Marketing |
| OPS | Operations |
| SALES | Sales |
| ADMIN | Administration |
| R&D | Research & Development |

---

**Notes:**
- Reverse charge VAT applies to most software and digital services purchased from outside the UK
- Insurance premiums are VAT-exempt — do not reclaim input VAT
- When unsure of the correct code, use 6900 (Miscellaneous) and flag for review
