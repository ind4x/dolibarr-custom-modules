# Dolibarr ERP Custom Modules

This repository contains enterprise extensions for the Dolibarr ERP/CRM ecosystem
engineered to automate financial workflows, accounting reconciliations, and operational
field reporting during an enterprise software engineering engagement at HTBS Africa.

---

## Architectural Overview

```text
+---------------------------------------------------------------+
|                      Dolibarr ERP Core                        |
|   Hook Manager, Action Triggers & Navigation HUD              |
+---------------------------------------------------------------+
            |                   |                   |
            v                   v                   v
+-----------------------+ +-------------------+ +-----------------------+
|  Treasury & Cashflow  | | Payment Split     | | Tax Calculation Engine|
|  - Liquidity Forecast | | & Ventilation     | | - Dynamic TVA & Rates |
|  - Real-Time Balance  | | - Multi-Account   | | - Invoice Integration |
+-----------------------+ +-------------------+ +-----------------------+
                                        |
                                        v
                            +-----------------------+
                            | Field Intervention    |
                            | - Dynamic PDF / ODT   |
                            | - Automated Signatures|
                            +-----------------------+
```

---

## Core Modules

### 1. Treasury Management (`modTresorerie`)
- Advanced cash-flow tracking and multi-account liquidity forecasting.
- Real-time reconciliation of expected payables vs receivables with visual alerting on balance depletion.

### 2. Payment Split & Ventilation (`modVentilation`)
- Automated accounting allocation (ventilation) across multiple bank accounts and project cost centers.
- Multi-currency splitting with automated differential ledger balance updates.

### 3. Custom Taxation Engine (`modTaxEngine`)
- Dynamic tax rule configuration supporting custom regional tax labels (TVA, GST, VAT) and exemptions on a per-line invoice basis.

### 4. Intervention Report Model (`modInterventionReport`)
- Automated field service generation compiling intervention logs, technician hours, and parts used into formal PDF documents.

---

## System Architecture

The modules strictly adhere to Dolibarr's modular architecture:
- **Descriptor Classes (`mod<ModuleName>.class.php`):** Declare database schema increments, user permissions, and admin dashboard hooks.
- **Hook & Trigger Handlers:** Intercept native CRUD cycles (`INVOICE_CREATE`, `PAYMENT_VALIDATE`, `LINEBILL_INSERT`) to inject business rules without modifying core engine source code.
- **Encapsulated Data Models:** Dedicated DAO (Data Access Object) classes wrapping SQL queries with parameter binding.

---

## Deployment & Installation

### Prerequisites
- Dolibarr ERP/CRM (v14.0 to v19.x)
- PHP 7.4, 8.1, or 8.2 (LAMP / LEMP stack)
- MySQL 5.7+ or MariaDB 10.4+

### Installation Steps
1. Navigate to your Dolibarr `custom` directory:
   ```bash
   cd /path/to/dolibarr/htdocs/custom/
   ```
2. Clone the modules repository:
   ```bash
   git clone git@github.com:ind4x/dolibarr-custom-modules.git
   ```
3. Grant appropriate web server ownership permissions:
   ```bash
   chown -R www-data:www-data dolibarr-custom-modules/
   ```
4. Access the Dolibarr administrative interface:
   - Navigate to **Home > Setup > Modules/Applications**.
   - Search for the custom modules and toggle them to **Active**.

---

## Technology Stack

- **ERP Framework:** Dolibarr ERP/CRM Core
- **Backend Language:** PHP 7.4+ / Object-Oriented PHP
- **Database:** MySQL, MariaDB (InnoDB, Foreign Key Constraints)
- **Templating & Reports:** QWeb, ODT, TCPDF

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Author

- **Author:** Youssef Fellah ([ind4x_](https://github.com/ind4x))
- **Institution:** Mundiapolis University, Engineering Cycle
