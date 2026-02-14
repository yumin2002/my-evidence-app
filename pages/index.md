---
title: Master Dashboard
---

<script>
  const rawOrders = [
    { order_datetime: '2026-01-16T10:00:00Z', category: 'Furniture', sales: 320 },
    { order_datetime: '2026-01-16T15:35:00Z', category: 'Technology', sales: 140 },
    { order_datetime: '2026-01-20T11:30:00Z', category: 'Office Supplies', sales: 180 },
    { order_datetime: '2026-01-24T09:15:00Z', category: 'Technology', sales: 410 },
    { order_datetime: '2026-01-28T13:00:00Z', category: 'Furniture', sales: 515 },
    { order_datetime: '2026-01-28T18:20:00Z', category: 'Office Supplies', sales: 205 },
    { order_datetime: '2026-02-01T16:45:00Z', category: 'Office Supplies', sales: 240 },
    { order_datetime: '2026-02-05T08:25:00Z', category: 'Technology', sales: 560 },
    { order_datetime: '2026-02-05T19:10:00Z', category: 'Furniture', sales: 190 },
    { order_datetime: '2026-02-08T14:00:00Z', category: 'Furniture', sales: 390 },
    { order_datetime: '2026-02-10T12:10:00Z', category: 'Office Supplies', sales: 270 },
    { order_datetime: '2026-02-13T09:05:00Z', category: 'Office Supplies', sales: 210 },
    { order_datetime: '2026-02-13T17:55:00Z', category: 'Technology', sales: 640 }
  ];

  const toDay = (isoDate) => {
    const d = new Date(isoDate);
    const y = d.getUTCFullYear();
    const m = String(d.getUTCMonth() + 1).padStart(2, '0');
    const day = String(d.getUTCDate()).padStart(2, '0');
    return `${y}-${m}-${day}`;
  };

  let startDate = '2026-01-16';
  let endDate = '2026-02-14';

  $: start = startDate ? new Date(`${startDate}T00:00:00Z`) : null;
  $: end = endDate ? new Date(`${endDate}T23:59:59Z`) : null;

  $: filteredOrders = rawOrders.filter((row) => {
    const t = new Date(row.order_datetime);
    const inStart = !start || t >= start;
    const inEnd = !end || t <= end;
    return inStart && inEnd;
  });

  $: trendMap = filteredOrders.reduce((acc, row) => {
    const day = toDay(row.order_datetime);
    acc[day] = (acc[day] || 0) + row.sales;
    return acc;
  }, {});

  $: sales_trend = Object.entries(trendMap)
    .map(([day, sales_usd]) => ({ day: new Date(`${day}T00:00:00Z`), sales_usd }))
    .sort((a, b) => a.day - b.day);
</script>

<div style="display:flex;gap:12px;align-items:end;margin-bottom:12px;">
  <label>
    Start Date
    <input type="date" bind:value={startDate} />
  </label>
  <label>
    End Date
    <input type="date" bind:value={endDate} />
  </label>
</div>
<LineChart
  title="Sales Trend (Filtered by Date Range)"
  data={sales_trend}
  x=day
  y=sales_usd
  xType=time
/>


<Grid cols=2>
  <BigValue title="Number of Leads" data={[{ value: 557 }]} value=value />
  <BigValue title="Number of Lead Replied" data={[{ value: 474 }]} value=value />
</Grid>

<Grid cols=2>
  <BigValue title="Average Call Duration (s)" data={[{ value: 35 }]} value=value />
  <BigValue title="Number of DND" data={[{ value: 0 }]} value=value />
</Grid>

<ECharts
  title="Appointment Count Per Status"
  config={{
    tooltip: { trigger: 'item' },
    legend: { orient: 'vertical', right: '4%', top: 'middle' },
    color: ['#56A8EA', '#28B7D9', '#6E86E7', '#8E73E4', '#4E7FEA'],
    series: [
      {
        type: 'pie',
        radius: ['58%', '78%'],
        center: ['30%', '50%'],
        label: { show: false },
        data: [
          { name: 'Confirmed - 119', value: 119 },
          { name: 'Noshow - 12', value: 12 },
          { name: 'Cancelled - 10', value: 10 },
          { name: 'New - 1', value: 1 },
          { name: 'Showed - 1', value: 1 }
        ]
      }
    ],
    graphic: {
      type: 'text',
      left: '26%',
      top: '46%',
      style: { text: '143', fontSize: 24, fontWeight: 600, fill: '#334155' }
    }
  }}
/>

<ECharts
  title="Total Number of Calls"
  config={{
    tooltip: { trigger: 'item' },
    legend: { orient: 'vertical', right: '4%', top: 'middle' },
    color: ['#56A8EA', '#28B7D9', '#6E86E7', '#8E73E4'],
    series: [
      {
        type: 'pie',
        radius: ['58%', '78%'],
        center: ['30%', '50%'],
        label: { show: false },
        data: [
          { name: 'Answered - 94', value: 94 },
          { name: 'Failed - 4', value: 4 },
          { name: 'Busy - 3', value: 3 },
          { name: 'Missed/No answer - 2', value: 2 }
        ]
      }
    ],
    graphic: {
      type: 'text',
      left: '26%',
      top: '46%',
      style: { text: '103', fontSize: 24, fontWeight: 600, fill: '#334155' }
    }
  }}
/>

<BarChart
  title="Appointments Per Month"
  data={[
    { month: 'Jan 26', count: 123 },
    { month: 'Feb 26', count: 70 }
  ]}
  x=month
  y=count
/>

<BigValue title="Lead-to-Appointment Conversion" data={[{ value: 0.2638 }]} value=value fmt=pct2 />
