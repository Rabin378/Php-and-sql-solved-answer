# Web Programming 2 (505514) — Midterm Practical Lab Solutions

Solutions to the 22-task midterm practical lab (130 points) for **Web Programming 2 (505514)**, covering **core PHP 8+** and **introductory SQL**. Every PHP page is designed to run on a local **XAMPP** server (Apache + MySQL + PHP 8.1+).

The repository also includes the original question packet in `docs/` so each solution can be checked against its requirements.

---

## Table of Contents

- [Repository Structure](#repository-structure)
- [Question Index](#question-index)
- [Getting Started](#getting-started)
- [Testing the Pages](#testing-the-pages)
- [Concepts Demonstrated](#concepts-demonstrated)
- [Verification](#verification)
- [Known Issues](#known-issues)

---

## Repository Structure

```text
web-programming-2-midterm/
├── README.md
├── docs/
│   └── Midterm_Practical_Lab_Packet.pdf      # Original question packet
├── database/
│   └── webprog2_midterm_setup.sql            # Shared setup script (Q15–18, Q20–22)
├── q01_invoice_calc.php                      # Q1
├── q02_gradebook.php                         # Q2
├── q03_shipping_tier.php                     # Q3
├── q04_http_status_matcher.php               # Q4
├── q05_loan_amortization.php                 # Q5
├── q06_layout_includes/                      # Q6
│   ├── config.php
│   ├── header.php
│   ├── footer.php
│   └── index.php
├── q07_pricing_functions.php                 # Q7
├── q08_functions.php                         # Q8
├── q08_strict_shipping.php                   # Q8
├── q09_sku_generator.php                     # Q9
├── q10_theme_switcher.php                    # Q10
├── q11_feedback_form.php                     # Q11
├── q12_ticket_order.php                      # Q12
├── q13_account_setup.php                     # Q13
├── q14_guestbook_preview.php                 # Q14
├── q14_thankyou.php                          # Q14
├── q15_books_schema.sql                      # Q15
├── q16_catalog_queries.sql                   # Q16
├── q17_pagination_queries.sql                # Q17
├── q18_aggregate_queries.sql                 # Q18
├── q19_functions.php                         # Q19
├── q19_log_analyzer.php                      # Q19
├── q20_functions.php                         # Q20
├── q20_course_finder.php                     # Q20
├── q20_course_queries.sql                    # Q20
├── q21_quote_builder.php                     # Q21
├── q21_quote_success.php                     # Q21
├── q21_quote_queries.sql                     # Q21
├── q22_functions.php                         # Q22
├── q22_store_explorer.php                    # Q22
├── q22_order_confirmed.php                   # Q22
└── q22_explorer_queries.sql                  # Q22
```

---

## Question Index

**Status legend:** ✅ matches the packet · ⚠️ works, with a minor deviation · ❌ bug, needs a fix (see [Known Issues](#known-issues))

| Q | Topic | Points | File(s) | Status |
|---|-------|:------:|---------|:------:|
| 1 | Order invoice calculator & type inspector | 5 | `q01_invoice_calc.php` | ✅ |
| 2 | Student gradebook array processor | 5 | `q02_gradebook.php` | ✅ |
| 3 | Shipping rate decision engine | 5 | `q03_shipping_tier.php` | ✅ |
| 4 | HTTP status dispatcher (`match`) | 5 | `q04_http_status_matcher.php` | ⚠️ |
| 5 | Loops showdown (`for`, `while`, `do…while`) | 5 | `q05_loan_amortization.php` | ✅ |
| 6 | Modular page architecture (`require_once`, `include`) | 5 | `q06_layout_includes/` | ✅ |
| 7 | Custom pricing functions, defaults & PHPDoc | 5 | `q07_pricing_functions.php` | ⚠️ |
| 8 | Strict types, nullable types & named arguments | 5 | `q08_functions.php`, `q08_strict_shipping.php` | ✅ |
| 9 | Static variable scope & built-in string functions | 5 | `q09_sku_generator.php` | ✅ |
| 10 | Query strings, `$_GET` & allowed-list validation | 5 | `q10_theme_switcher.php` | ✅ |
| 11 | HTML form, `$_POST`, length validation & sticky inputs | 5 | `q11_feedback_form.php` | ⚠️ |
| 12 | Ticket order with `filter_var()` | 5 | `q12_ticket_order.php` | ✅ |
| 13 | Password rules & checkbox array validation | 5 | `q13_account_setup.php` | ✅ |
| 14 | XSS defense & redirect-after-success | 5 | `q14_guestbook_preview.php`, `q14_thankyou.php` | ❌ |
| 15 | Table design, keys & data types | 5 | `q15_books_schema.sql` | ✅ |
| 16 | `SELECT`, `WHERE`, `ORDER BY` | 5 | `q16_catalog_queries.sql` | ✅ |
| 17 | Pagination with `LIMIT` / `OFFSET` | 5 | `q17_pagination_queries.sql` | ✅ |
| 18 | Aggregate functions | 5 | `q18_aggregate_queries.sql` | ⚠️ |
| 19 | Challenge: server access log analyzer | 10 | `q19_functions.php`, `q19_log_analyzer.php` | ✅ |
| 20 | Mini-app 1: university course finder & tuition | 10 | `q20_functions.php`, `q20_course_finder.php`, `q20_course_queries.sql` | ❌ |
| 21 | Mini-app 2: hardware B2B quote builder | 10 | `q21_quote_builder.php`, `q21_quote_success.php`, `q21_quote_queries.sql` | ✅ |
| 22 | Mini-app 3: storefront explorer & quick-order redirect | 10 | `q22_functions.php`, `q22_store_explorer.php`, `q22_order_confirmed.php`, `q22_explorer_queries.sql` | ✅ |

**Total: 130 points** (Part 1 = 30, Part 2 = 40, Part 3 = 20, Part 4 = 40).

---

## Getting Started

### Prerequisites

- [XAMPP](https://www.apachefriends.org/) with **PHP 8.1+** (the code itself needs PHP 8.0 or newer)
- A web browser

### 1. Place the project in `htdocs`

Clone or copy this repository into a folder named `midterm_lab` inside your XAMPP `htdocs` directory:

| OS | Path |
|----|------|
| Windows | `C:\xampp\htdocs\midterm_lab\` |
| macOS | `/Applications/XAMPP/htdocs/midterm_lab/` |

```bash
git clone https://github.com/<your-username>/web-programming-2-midterm.git midterm_lab
```

### 2. Start the services

Open the **XAMPP Control Panel** and start **Apache** (for PHP) and **MySQL** (for SQL).

### 3. Create the shared database

The SQL tasks (Q15–Q18, Q20–Q22) use the `webprog2_midterm` database.

1. Open **phpMyAdmin** at <http://localhost/phpmyadmin>.
2. Click the **SQL** tab.
3. Paste the contents of `database/webprog2_midterm_setup.sql` and click **Go**.

This creates the `products` table (12 rows) and the `courses` table (8 rows).

### 4. Run the PHP pages

Open a page in your browser at `http://localhost/midterm_lab/<filename>.php`.

---

## Testing the Pages

Most PHP pages render with no query string. The interactive pages below are worth testing with the listed inputs.

| Question | URL | What to check |
|----------|-----|---------------|
| Q1 | `/midterm_lab/q01_invoice_calc.php` | Subtotal `$269.97`, Grand Total `$291.57`, `Loose Match: true`, `Strict Match: false` |
| Q3 | `/midterm_lab/q03_shipping_tier.php` | Base Cost `$12.50`, Surcharge `$4.50`, Total `$17.00` |
| Q6 | `/midterm_lab/q06_layout_includes/index.php` | Page renders with no redeclaration errors |
| Q10 | `/midterm_lab/q10_theme_switcher.php?theme=dark&size=large` | Dark theme, large font |
| Q10 | `/midterm_lab/q10_theme_switcher.php?theme=neon&size=giant` | Warnings shown; falls back to `light` / `medium` |
| Q11 | `/midterm_lab/q11_feedback_form.php` | Submit `A` and `Too short` → errors, values stay in the form |
| Q12 | `/midterm_lab/q12_ticket_order.php` | Email `user@example.com`, 2 tickets, donation `15.50` → `Total Due: $105.50` |
| Q13 | `/midterm_lab/q13_account_setup.php` | Weak password + 2 tracks → errors, password cleared, tracks still checked |
| Q14 | `/midterm_lab/q14_guestbook_preview.php` | Preview / Submit Final buttons; `Submit Final` redirects to `q14_thankyou.php?user=…` |
| Q19 | `/midterm_lab/q19_log_analyzer.php?method=POST&min_ms=100` | `Matching Entries: 2 \| Average Response Time: 800.0 ms` |
| Q20 | `/midterm_lab/q20_course_finder.php?dept=CS` | See [Known Issues](#known-issues) — tuition values are incorrect |
| Q21 | `/midterm_lab/q21_quote_builder.php` | Valid submission redirects to `q21_quote_success.php?company=…&items=…&qty=…&total=…` |
| Q22 | `/midterm_lab/q22_store_explorer.php?category=Audio&max_price=100` | `Matches: 1 \| Avg Price: $64.00` |

### Running the SQL files

Open each `.sql` file in the phpMyAdmin **SQL** tab (or paste its contents) and click **Go**. Each file starts with `USE webprog2_midterm;`, so run the shared setup script first.

Expected results for the SQL queries:

| File | Key result |
|------|------------|
| `q15_books_schema.sql` | `book_id` shows `PRI` / `auto_increment`; `retail_price` is `decimal(6,2)`; `in_print` defaults to `1` |
| `q16_catalog_queries.sql` | Query A: 4 rows (HW-103, HW-110, HW-101, HW-105) · Query B: 3 rows · Query C: 2 SSD rows |
| `q17_pagination_queries.sql` | Pages 1–3 return HW-101→HW-104, HW-105→HW-108, HW-109→HW-112; Query D returns HW-109, HW-111, HW-104 |
| `q18_aggregate_queries.sql` | Query A: `total_products 12`, `total_units 468`, `avg_price 128.075000`. Query B: `online_course_count 3`, `total_online_seats 98` |
| `q20_course_queries.sql` | CS courses: `530.00`, `420.00`, `555.00`, `570.00` (by fee order) |
| `q21_quote_queries.sql` | Query 1: HW-103, HW-107, HW-101 · Query 2: HW-107, HW-110, HW-103 |
| `q22_explorer_queries.sql` | Query 1: `total_matches 8`. Query 2: HW-109, HW-111, HW-104 |

---

## Concepts Demonstrated

| Concept | Where to look |
|---------|---------------|
| Scalar types, `gettype()`, loose (`==`) vs strict (`===`) comparison | `q01` |
| Indexed & associative arrays, `foreach` | `q02`, `q09`, `q19`, `q20`, `q22` |
| `if` / `elseif` / `else`, `switch` with `break` | `q03` |
| PHP 8 `match` expressions (value, multi-arm, `match(true)`) | `q04`, `q19`, `q20`, `q21`, `q22` |
| `for`, `while`, `do…while` | `q05` |
| `require_once`, `include`, `__DIR__` | `q06_layout_includes/` |
| Default parameters, return types | `q07`, `q20` |
| `declare(strict_types=1)`, nullable types (`?string`), named arguments | `q08`, `q19`, `q20`, `q22` |
| `static` local variables | `q09` |
| `$_GET`, `$_POST`, `$_SERVER['REQUEST_METHOD']`, `??` | `q10`–`q14`, `q19`–`q22` |
| Allowed-list validation with `in_array(..., true)` | `q10`, `q13`, `q19`, `q20`, `q22` |
| `filter_var()` with `FILTER_VALIDATE_INT`, `FILTER_VALIDATE_FLOAT`, `FILTER_VALIDATE_EMAIL` | `q12`, `q19`, `q22` |
| Checkbox arrays (`name="topics[]"`, `name="product_ids[]"`) | `q13`, `q21` |
| Sticky form values (repopulating inputs after a validation error) | `q11`, `q12`, `q13`, `q14`, `q20`–`q22` |
| XSS escaping with `htmlspecialchars(…, ENT_QUOTES, 'UTF-8')` | Every page that outputs user data |
| Redirect-after-success: `urlencode()` / `http_build_query()` + `header('Location: …')` + `exit` | `q14`, `q21`, `q22` |
| SQL `CREATE TABLE`, `PRIMARY KEY`, `AUTO_INCREMENT`, `DECIMAL`, `DEFAULT` | `q15` |
| SQL `SELECT`, `WHERE`, `BETWEEN`, `IN`, `LIKE`, `ORDER BY` | `q16`, `q20`, `q21`, `q22` |
| SQL `LIMIT` / `OFFSET` pagination | `q17`, `q22` |
| SQL aggregates `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` with aliases | `q18`, `q22` |

**Ground rules followed:** no frameworks, no Composer, no PDO/mysqli, no sessions or cookies, and `DECIMAL` (not `FLOAT`) for all currency columns.

---

## Verification

The solutions were checked in a local environment against the expected outputs in the question packet:

- **PHP:** every `.php` file passes `php -l` (syntax check) with PHP 8.3. Every page was loaded with no query string to check for warnings, and the interactive pages (valid and invalid inputs, POST submissions, and redirects) were exercised over HTTP and compared with the packet.
- **SQL:** the shared setup script was run on MariaDB 10.11, and every `.sql` file executed without errors. Result sets were compared with the packet's expected output.

Results that do not match the packet are documented under [Known Issues](#known-issues).

---

## Known Issues

These are the deviations found during testing. Items marked ❌ above need a fix before they match the packet.

1. **Q20 tuition formula is wrong** (`q20_functions.php`). The function's parameter is named `$abfee`, but the body uses `$labFee`, which is undefined. The formula also adds `$credits + $creditRate` instead of multiplying. As a result, CS101 shows `$124.00` instead of `$530.00`, and PHP emits an "Undefined variable `$labFee`" warning for every row. *Fix:* rename the parameter to `$labFee` and return `($credits * $creditRate) + $labFee`. The companion SQL (`q20_course_queries.sql`) is correct.

2. **Q14 preview does not show the message** (`q14_guestbook_preview.php`). The preview box renders only the username. In addition, message validation allows up to 500 characters, while the packet and the form label specify 200. The `<meta>` and `<title>` tags also sit outside `<head>`.

3. **Q7 is missing PHPDoc blocks.** The functions use `//` comments instead of `/** … */` blocks with `@param` and `@return` tags, which the packet requires.

4. **`strlen()` counts bytes, not characters** (`q11`, `q14`, `q20`, `q21`). In UTF-8, Korean characters take 3 bytes each, so a one-character name such as `김` passes the 2-character minimum in Q11. Use `mb_strlen($value, 'UTF-8')` instead.

5. **Q8 function name casing.** The function is declared as `buildshippingLabel` but called as `buildShippingLabel`. This works because PHP function names are case-insensitive, but the names should match. The output also prints `NO` for express and `No` for fragile; use one format for both.

6. **Q22 dataset does not match the database.** The PHP dataset has 7 products, while the database has 12. As a result, `max_price=100` shows 5 matches on the PHP page but the SQL query returns 8.

7. **Q18 expected value in the packet is incorrect.** The packet lists `total_inventory_value: 27482.55`, but its own seed data sums to `27367.36`. The query is correct; the packet figure is not.

8. **Q4 capitalization.** The output reads `Success: Request Completed` and `Server Error: Internal Failure`, while the packet uses lowercase words after the colon.

9. **Q19 out-of-range `min_ms` is reset silently.** A value outside 0–5000 falls back to `0` without an error message.

10. **Q21 minor formatting.** Product prices display as `$329` instead of `$329.00`, and the checkbox `value` attribute is not wrapped in `htmlspecialchars()`.

---

## Reference

- Course: Web Programming 2 (505514)
- Question packet: [`docs/Midterm_Practical_Lab_Packet.pdf`](docs/Midterm_Practical_Lab_Packet.pdf)
