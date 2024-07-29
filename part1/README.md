# Making BaseLine Basic Chart

## Step 1. Assign width & height

## Step 2. Set up x and y scales

It fits into you know the pixel scale on your screen or in your browser

```javascript
const x = d3.scaleTime().range([0, width]);
const y = d3.scaleLinear().range([height, 0]);
```

## Step 3. Create SVG element and append chart container

Using d3 select method to grab chart contianer 

```javascript
const svg = d3.select('#chart-container')
              .append('svg')
              .attr('width', width + margin.left + margin.right)
              .attr('height', height + margin.top + margin.bottom)
              .append('g')
              .attr('transform', `translate(${margin.left}, ${margin.top})`);
```

## Step 4. Create fake dataset

## Step 5. Define x and y domains

Domain means what data is going to fit into the range we declared

```javascript
x.domain(d3.extent(dataset, d => d.date));
y.domain([0, d3.max(dataset, d => d.value)]);
```

## Step 6. Add the x-axis and y-axis

We're going to call our SVG that we've already been developing and append a new group element

```javascript
svg.append('g')
   .attr('transform', `translate(0, ${height})`)
   .call(d3.axisBottom(x)
    .ticks(d3.timeMonth.every(1))
    .tickFormat(d3.timeFormat('%b %Y')));
```

```javascript
svg.append('g')
   .call(d3.axisLeft(y));
```

## Step 7. Create the line Generator
```javascript
const line = d3.line()
               .x(d => x(d.date))
               .y(d => y(d.value));
```

## Step 8. Add the line path to the SVG element
```javascript
svg.append('path')
  .datum(dataset)
  .attr('fill', 'none')
  .attr('stroke', 'steelblue')
  .attr('stroke-width', 1)
  .attr('d', line);
```