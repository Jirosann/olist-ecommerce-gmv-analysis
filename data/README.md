# Data

The CSV files are not stored in this repository. Download them from Kaggle and place them as shown below.

## Sources

| Dataset | Kaggle page | License |
|---|---|---|
| Brazilian E-Commerce Public Dataset by Olist | https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce | CC BY-NC-SA 4.0 |
| Marketing Funnel by Olist | https://www.kaggle.com/datasets/olistbr/marketing-funnel-olist | CC BY-NC-SA 4.0 |

Both datasets are published by Olist. Orders cover September 2016 to October 2018; the marketing funnel covers leads first contacted between June 2017 and May 2018.

## Expected layout

```
data/
  ecommerce_olist/
    olist_customers_dataset.csv
    olist_orders_dataset.csv
    olist_order_items_dataset.csv
    olist_order_payments_dataset.csv
    olist_order_reviews_dataset.csv
    olist_products_dataset.csv
    olist_sellers_dataset.csv
  marketing_funnel/
    olist_marketing_qualified_leads_dataset.csv
    olist_closed_deals_dataset.csv
```

The Kaggle archive for the e-commerce dataset also contains `olist_geolocation_dataset.csv` and `product_category_name_translation.csv`. The notebook does not use them, so you can leave them out.

## Download with the Kaggle CLI (optional)

```bash
kaggle datasets download -d olistbr/brazilian-ecommerce -p data/ecommerce_olist --unzip
kaggle datasets download -d olistbr/marketing-funnel-olist -p data/marketing_funnel --unzip
```

## Tables and joins

| File | Rows | Key columns |
|---|---|---|
| olist_orders_dataset.csv | 99,441 | order_id, customer_id |
| olist_order_items_dataset.csv | 112,650 | order_id, product_id, seller_id |
| olist_order_payments_dataset.csv | 103,886 | order_id |
| olist_order_reviews_dataset.csv | 99,224 | order_id |
| olist_customers_dataset.csv | 99,441 | customer_id, customer_unique_id |
| olist_products_dataset.csv | 32,951 | product_id |
| olist_sellers_dataset.csv | 3,095 | seller_id |
| olist_marketing_qualified_leads_dataset.csv | 8,000 | mql_id |
| olist_closed_deals_dataset.csv | 842 | mql_id, seller_id |

- `orders` joins to `order_items`, `order_payments` and `order_reviews` on `order_id`, and to `customers` on `customer_id`.
- `customer_unique_id` identifies a person across orders (each order gets its own `customer_id`).
- `order_items` joins to `products` on `product_id` and to `sellers` on `seller_id`.
- `marketing_qualified_leads` joins to `closed_deals` on `mql_id`; `closed_deals.seller_id` links a converted lead to the e-commerce tables.
