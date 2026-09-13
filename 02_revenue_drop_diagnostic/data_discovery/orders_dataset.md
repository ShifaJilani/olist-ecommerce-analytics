# Orders Dataset — Data Discovery

## 1. Dataset Overview

**Source:** [Olist Brazilian E-Commerce Public Dataset — Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce?select=olist_orders_dataset.csv)

**File:** `olist_orders_dataset.csv`

This is the core order-level dataset in the Olist Brazilian E-Commerce Public Dataset.

It contains information about orders, including:
- customer
- order status
- purchase time
- approval time
- carrier delivery
- customer delivery
- estimated delivery

### Basic Structure

| Check | Finding |
|---|---:|
| Total rows | **99,441** |
| Total columns | **8** |
| Unique `order_id` | **99,441** |
| Missing `customer_id` | **0** |
| Duplicate `order_id` | **0** |

### Table Grain

**1 row = 1 order**

The number of rows and unique `order_id`s are both **99,441**, confirming that each order appears once in this table.

---

## 2. Columns

| Column | Data Type | Description |
|---|---|---|
| `order_id` | Text | Unique identifier for an order |
| `customer_id` | Text | Identifier of the customer who placed the order |
| `order_status` | Text | Current/status stage of the order |
| `order_purchase_timestamp` | Date/Time | Date and time when the order was placed |
| `order_approved_at` | Date/Time | Date and time when the order was approved |
| `order_delivered_carrier_date` | Date/Time | Date and time when the order was handed to the carrier |
| `order_delivered_customer_date` | Date/Time | Date and time when the order was delivered to the customer |
| `order_estimated_delivery_date` | Date/Time | Estimated date of delivery |

---

## 3. Missing Values

| Column | Missing Values |
|---|---:|
| `order_id` | **0** |
| `customer_id` | **0** |
| `order_status` | **0** |
| `order_purchase_timestamp` | **0** |
| `order_approved_at` | **160** |
| `order_delivered_carrier_date` | **1,783** |
| `order_delivered_customer_date` | **2,965** |
| `order_estimated_delivery_date` | **0** |

### Observation

The core order information (`order_id`, `customer_id`, `order_status`, and `order_purchase_timestamp`) has **no missing values**.

The missing values are concentrated in the **order approval and delivery-related dates**.

---

## 4. Date Ranges

| Column | Earliest Date | Latest Date |
|---|---|---|
| `order_purchase_timestamp` | **4 Sep 2016 21:15** | **17 Oct 2018 17:30** |
| `order_approved_at` | **15 Sep 2016 12:16** | **3 Sep 2018 17:40** |
| `order_delivered_carrier_date` | **8 Oct 2016 10:34** | **11 Sep 2018 19:48** |
| `order_delivered_customer_date` | **11 Oct 2016 13:46** | **17 Oct 2018 13:22** |
| `order_estimated_delivery_date` | **30 Sep 2016** | **12 Nov 2018** |

### Observation

`order_purchase_timestamp` provides a complete order timeline from **September 2016 to October 2018**.

The estimated delivery date extends to **November 2018**, beyond the last purchase date.

---

## 5. Order Status Distribution

| `order_status` | Number of Orders |
|---|---:|
| delivered | **96,478** |
| shipped | **1,107** |
| canceled | **625** |
| unavailable | **609** |
| invoiced | **314** |
| processing | **301** |
| created | **5** |
| approved | **2** |
| **Total** | **99,441** |

### Observation

The dataset contains orders at **different stages of the order process**.

The large majority of orders are marked **`delivered` (96,478)**.

---

## 6. Uniqueness Checks

### `order_id`

- Total rows: **99,441**
- Unique `order_id`s: **99,441**
- Duplicate `order_id`s: **0**

**Observation:** `order_id` is unique in the dataset.

### `customer_id`

- Missing values: **0**
- Duplicate values: **0**

**Observation:** Each `customer_id` appears only once in this orders dataset.

---

## 7. Date Consistency Checks

### 7.1 `order_purchase_timestamp` → `order_approved_at`

The check compared:

`order_approved_at` < `order_purchase_timestamp`

Results:

| Result | Count |
|---|---:|
| OK | **99,281** |
| Missing approval | **160** |
| Actual date errors | **0** |
| **Total** | **99,441** |

**Observation:** No orders with both dates available had an approval timestamp earlier than the purchase timestamp.

The **160 missing approval timestamps** account for the missing cases.

---

### 7.2 `order_approved_at` → `order_delivered_carrier_date`

The check compared:

`order_delivered_carrier_date` < `order_approved_at`

Results:

| Result | Count |
|---|---:|
| OK | **96,285** |
| Inconsistent date sequence | **1,359** |
| Missing approval | **160** |
| Missing carrier date | **1,637** |
| **Total** | **99,441** |

**Observation:** **1,359 orders (1.37%)** have an `order_delivered_carrier_date` earlier than their `order_approved_at`.

---

### 7.3 Missing Carrier and Customer Delivery Dates

A separate check was performed to understand the relationship between the missing delivery dates.

| Situation | Count |
|---|---:|
| Both dates missing | **1,782** |
| Both dates present | **96,475** |
| Only `order_delivered_carrier_date` missing | **1** |
| Only `order_delivered_customer_date` missing | **1,183** |
| **Total** | **99,441** |

This confirms:

- `order_delivered_carrier_date` missing = **1,782 + 1 = 1,783**
- `order_delivered_customer_date` missing = **1,782 + 1,183 = 2,965**

**Observation:** The original missing-value counts are consistent.

---

### 7.4 `order_delivered_carrier_date` → `order_delivered_customer_date`

The check compared:

`order_delivered_customer_date` < `order_delivered_carrier_date`

Results:

| Result | Count |
|---|---:|
| OK | **96,452** |
| Inconsistent date sequence | **23** |
| Missing carrier date | **1,783** |
| Missing customer delivery date | **1,183** |
| **Total** | **99,441** |

**Observation:** **23 orders** have a customer delivery date earlier than the carrier delivery date.

---

### 7.5 `order_delivered_customer_date` → `order_estimated_delivery_date`

The check compared:

`order_delivered_customer_date` > `order_estimated_delivery_date`

Results:

| Result | Count |
|---|---:|
| On time | **88,649** |
| Late | **7,827** |
| Missing customer delivery date | **2,965** |
| **Total** | **99,441** |

**Observation:** **7,827 orders** were delivered after their estimated delivery date.

---

## 8. Key Discovery Findings

From the initial discovery of `olist_orders_dataset.csv`:

1. The table contains **99,441 unique orders**.
2. **1 row represents 1 order**.
3. `order_purchase_timestamp` is complete and covers **September 2016 to October 2018**.
4. Approval and delivery-related columns contain missing values.
5. There are **1,359 orders (1.37%)** with an inconsistent approval-to-carrier date sequence.
6. There are **23 orders** with an inconsistent carrier-to-customer delivery date sequence.
7. **7,827 orders** were delivered after the estimated delivery date.
8. The dataset contains **8 different order statuses**, with **96,478 orders marked as delivered**.

---

## 9. Discovery Status

**Status: Completed**

This file has been reviewed for:

- Structure
- Row count
- Column count
- Table grain
- Uniqueness
- Missing values
- Date ranges
- Order-status distribution
- Date consistency
