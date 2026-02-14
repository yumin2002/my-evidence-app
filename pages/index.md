---
title: Master Dashboard (JSON Render)
---

<script>
  // Frontend-only dummy JSON data (no SQL in markdown)
  const rows = [
    { month: '2026-01', category: 'Furniture', sales_usd: 1200 },
    { month: '2026-01', category: 'Technology', sales_usd: 980 },
    { month: '2026-01', category: 'Office Supplies', sales_usd: 430 },
    { month: '2026-02', category: 'Furniture', sales_usd: 1575 },
    { month: '2026-02', category: 'Technology', sales_usd: 1320 },
    { month: '2026-02', category: 'Office Supplies', sales_usd: 510 },
    { month: '2026-03', category: 'Furniture', sales_usd: 990 },
    { month: '2026-03', category: 'Technology', sales_usd: 1750 },
    { month: '2026-03', category: 'Office Supplies', sales_usd: 620 }
  ];

  const total_sales = rows.reduce((acc, row) => acc + row.sales_usd, 0);
  const summary = [{ total_sales }];
</script>

# Master Dashboard

<BigValue
  data={summary}
  title="Total Sales"
  value=total_sales
  fmt=usd0
/>

<BarChart
  data={rows}
  title="Sales by Month (JSON)"
  x=month
  y=sales_usd
  series=category
/>
