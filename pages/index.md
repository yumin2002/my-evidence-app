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

  $: start = inputs?.date_range?.start ? new Date(`${inputs.date_range.start}T00:00:00Z`) : null;
  $: end = inputs?.date_range?.end ? new Date(`${inputs.date_range.end}T23:59:59Z`) : null;
  $: trendRows = rawOrders.filter((row) => (!start || row.order_time >= start) && (!end || row.order_time <= end));
</script>

<DateRange name="date_range" />
<LineChart
  title="Sales Trend (Filtered by Date Range)"
  data={trendRows}
  x=order_time
  y=sales
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
