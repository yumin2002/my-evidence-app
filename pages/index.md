---
title: Master Dashboard
---

<DateRange name="date_range" defaultValue="last30Days" />

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
