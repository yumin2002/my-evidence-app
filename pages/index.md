---
title: Master Dashboard
---

<script>
  const rawOrders = [
    { order_time: new Date('2026-01-16T10:00:00Z'), category: 'Furniture', sales: 320 },
    { order_time: new Date('2026-01-16T15:35:00Z'), category: 'Technology', sales: 140 },
    { order_time: new Date('2026-01-20T11:30:00Z'), category: 'Office Supplies', sales: 180 },
    { order_time: new Date('2026-01-24T09:15:00Z'), category: 'Technology', sales: 410 },
    { order_time: new Date('2026-01-28T13:00:00Z'), category: 'Furniture', sales: 515 },
    { order_time: new Date('2026-01-28T18:20:00Z'), category: 'Office Supplies', sales: 205 },
    { order_time: new Date('2026-02-01T16:45:00Z'), category: 'Office Supplies', sales: 240 },
    { order_time: new Date('2026-02-05T08:25:00Z'), category: 'Technology', sales: 560 },
    { order_time: new Date('2026-02-05T19:10:00Z'), category: 'Furniture', sales: 190 },
    { order_time: new Date('2026-02-08T14:00:00Z'), category: 'Furniture', sales: 390 },
    { order_time: new Date('2026-02-10T12:10:00Z'), category: 'Office Supplies', sales: 270 },
    { order_time: new Date('2026-02-13T09:05:00Z'), category: 'Office Supplies', sales: 210 },
    { order_time: new Date('2026-02-13T17:55:00Z'), category: 'Technology', sales: 640 }
  ];
  const rawReplies = [
    { order_time: new Date('2026-01-16T12:00:00Z'), replies: 22 },
    { order_time: new Date('2026-01-20T12:00:00Z'), replies: 26 },
    { order_time: new Date('2026-01-24T12:00:00Z'), replies: 31 },
    { order_time: new Date('2026-01-28T12:00:00Z'), replies: 35 },
    { order_time: new Date('2026-02-01T12:00:00Z'), replies: 29 },
    { order_time: new Date('2026-02-05T12:00:00Z'), replies: 41 },
    { order_time: new Date('2026-02-08T12:00:00Z'), replies: 33 },
    { order_time: new Date('2026-02-10T12:00:00Z'), replies: 30 },
    { order_time: new Date('2026-02-13T12:00:00Z'), replies: 44 }
  ];

  $: start = inputs?.date_range?.start ? new Date(`${inputs.date_range.start}T00:00:00Z`) : null;
  $: end = inputs?.date_range?.end ? new Date(`${inputs.date_range.end}T23:59:59Z`) : null;
  $: trendRows = rawOrders.filter((row) => (!start || row.order_time >= start) && (!end || row.order_time <= end));
  $: replyTrendRows = rawReplies.filter((row) => (!start || row.order_time >= start) && (!end || row.order_time <= end));
</script>

<DateRange name="date_range" />
<Grid cols=2>
  <LineChart
    title="Sales Trend (Filtered by Date Range)"
    data={trendRows}
    x=order_time
    y=sales
    xType=time
  />
  <LineChart
    title="Replies Trend (Same Date Filter)"
    data={replyTrendRows}
    x=order_time
    y=replies
    xType=time
  />
</Grid>


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
    series: [
      {
        type: 'pie',
        data: [
          { name: 'Confirmed - 119', value: 119 },
          { name: 'Noshow - 12', value: 12 },
          { name: 'Cancelled - 10', value: 10 },
          { name: 'New - 1', value: 1 },
          { name: 'Showed - 1', value: 1 }
        ]
      }
    ]
  }}
/>

<ECharts
  title="Total Number of Calls"
  config={{
    tooltip: { trigger: 'item' },
    series: [
      {
        type: 'pie',
        data: [
          { name: 'Answered - 94', value: 94 },
          { name: 'Failed - 4', value: 4 },
          { name: 'Busy - 3', value: 3 },
          { name: 'Missed/No answer - 2', value: 2 }
        ]
      }
    ]
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
