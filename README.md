# Learn Data Science by Analyzing COVID-19

COVID-19 has hit hard in the past year and its impact has been notorious both from a sanitary perspective and [an economic one](https://www.opentable.com/state-of-industry). Plenty has been written about it, especially statistical reports on its exponential growth and the importance of [“flattening the curve”](https://www.washingtonpost.com/graphics/2020/world/corona-simulator/).

At INE, we wanted to help raise awareness of the issues associated with the spread of COVID-19 by making a dynamic and interactive analysis of the situation using Python and Data Science.

We’ve made an [open source project](https://github.com/ine-rmotr-projects/analyzing-covid-19-outbreak) that you can fork and follow step by step. You can see the process that Data Scientists follow to analyze the situation and make predictions.

![worldwide-confirmed-cases](https://user-images.githubusercontent.com/7065401/110378187-07a76e00-8034-11eb-8a98-c197523e9a35.gif)

> This post is an update of our [last year's post](https://blog.rmotr.com/learn-data-science-by-analyzing-covid-19-27a063d7f442) with the same analysis but with the data of the whole last year.

Let's get started!

## Part 1: The Basics of Exploratory Data Analysis and Data Wrangling
We’ll start with the first Notebook, [`Part 1.ipynb`]() and follow the basic steps of every Data Science project.

### Step 1: Reading Data
The first step is getting the data. In this case, we’re using [this GitHub repo](https://github.com/CSSEGISandData/COVID-19) by Johns Hopkins University that contains CSV files updated daily.

We’re using a neat Pandas technique of reading the CSV directly from the Github repo, which means we can run our notebooks everyday and it’ll stay up to date:

```python
COVID_CONFIRMED_URL = 'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv'

covid_confirmed = pd.read_csv(COVID_CONFIRMED_URL)
```

### Step 2: Data Cleaning
This is the mandatory second step of our project. Here, the data is fairly clean, so there isn’t much more to do. We’ll replace a few country names and fill in blanks.

### Step 3 & 4: Analysis and Data Wrangling
In the first stage of analyzing, we’ll start with a worldwide impact analysis of COVID-19. To conduct our analysis, we’ll need to create new columns, create intermediate DataFrames, and re-shape (melt, stack, group) our data. This is usually known as the “Data Wrangling” process.

![10-total-cases](https://user-images.githubusercontent.com/7065401/110484704-ac27bf80-80c9-11eb-9d13-2cc47fa43e58.png)
> Proportion of cases that have been active, recovered or died.

We can then plot the evolution of cases over time which shows, as we know, an alarming exponential growth:

![exponential-growth](https://user-images.githubusercontent.com/7065401/110380543-03308480-8037-11eb-8889-609c8f1f36b6.png)

As you may know already, it’s hard to see if growth is slowing down when it’s exponential, so we’ll change our y-axis to use a logarithmic scale:

![log-growth](https://user-images.githubusercontent.com/7065401/110380539-01ff5780-8037-11eb-8ee2-5e3267818fdc.png)

In this case we case see that the curve is flattening, the exponential growth is lower than some months ago. 

To continue our analysis, we’ll compare **Recovery vs Mortality**. To do that, we’ll define a few new columns with “ratio every 100 confirmed cases”.

![recovery-ratio](https://user-images.githubusercontent.com/7065401/110379484-a385a980-8035-11eb-973b-2a8cce595e6e.png)

We see a more encouraging scenario where recovery has sped up and is kept at a constant rate, and deaths are lowing down week after week.

### Evolution of COVID-19, in a Dynamic Worldwide Map
We’ll finish the first part of our analysis with an interactive map showing the evolution of COVID-19 over time. The Notebook contains a dynamic plot you can play with, which looks like this:

![worldwide-confirmed-cases](https://user-images.githubusercontent.com/7065401/110378187-07a76e00-8034-11eb-8a98-c197523e9a35.gif)

The growth isns't as fast as some months ago.

## Part 2: More In-depth Analysis
In this second part, we’ll dig deeper into the state of each country. Head now to [`Part 2.ipynb`]() to follow the process step by step.

We’ll start again by reading the data, cleaning it, and creating a few intermediate DataFrames. You can see where this is going already.  **More than 70% of a Data Scientist’s time is spent on “Data Wrangling”**.

### Analysis of More Affected Countries
After more than a year since the virus is between us, we know that US, India, Brazil and Russia are the countries with the number higher of cases, as shown in the following charts:

![06-confirmed-cases](https://user-images.githubusercontent.com/7065401/110481905-d7f57600-80c6-11eb-9ff3-b3c8acafbe42.png)
> Total of confirmed cases per country

![07-deaths](https://user-images.githubusercontent.com/7065401/110482329-56521800-80c7-11eb-9114-6ffdc0bb2e99.png)
> Deaths per country

But can we go deeper? Our role as Data Scientists is to keep pushing past the surface of the data. The number of cases (confirmed, deaths, recovered) per country is publicly known. However, we can go further and create our own derived analysis. For example “mortality per country”, which now shows a different perspective:

![08-mortality-rate](https://user-images.githubusercontent.com/7065401/110482384-64a03400-80c7-11eb-84ad-daad3ccf43ef.png)
> Mortality per country

Finally, let’s take a look at the evolution of cases in these countries, in logarithmic scale (you can find a linear scale in the Notebook):

![09-evolution-log](https://user-images.githubusercontent.com/7065401/110482550-8d282e00-80c7-11eb-81c7-5d967742996e.png)
> Evolution per country, logarithmic scale

The cases are being stabilized.

### \<INSERT YOUR COUNTRY> Analysis

The beauty of “programmatic” analysis is that you can change one variable and have a dynamic analysis. For the sake of this post, I’ll use the USA, but you can spin [`Part 2.ipynb`]() and try with whatever country you call home.

First, we see a worrying “developing state” where the curve is "flat", but after that the slope increases.

![11-cases-us](https://user-images.githubusercontent.com/7065401/110485241-32dc9c80-80ca-11eb-9f94-eeecd51f38e5.png)
> Confirmed cases in the USA over the time

We can see the same data in logarithmic scale too. At the end we see what we could call "flattening the curve" where the cases are being stabilized thanks to all measures taken in recent months.

![12-cases-us-log](https://user-images.githubusercontent.com/7065401/110485250-340dc980-80ca-11eb-94c4-64b3f07d3a8f.png)
> Confirmed cases in the USA over the time, in logarithmic scale

And we can extend it per state:

![13-cases-us-state](https://user-images.githubusercontent.com/7065401/110485251-34a66000-80ca-11eb-9039-dfa128348cb0.png)
> COVID-19 confirmed cases per US State.

As you can see California, Texas, Florida and New York have been the most affected states.

## Part 3: Forecasting the Evolution of COVID-19

The last part of our project, [`Part 3.ipynb`]() shows how to implement a simple Linear Regression model to predict the evolution of COVID-19.

What we are going to do is try to fit the confirmed cases using that linear regression model and simulate how the curve of cases would behave if it followed this model distribution.

Let's use US confirmed cases and try to predict its behaviour for the next weeks:

![15-predict-us-log](https://user-images.githubusercontent.com/7065401/110488590-61a84200-80cd-11eb-8991-76385f1070b5.png)
> Predicted cases in the US, logarithmic scale

The trick to making this regression work understanding that this is not an actual linear process, but an exponential one. We must treat our data accordingly. We can change the y-axis to display our predictions in a linear scale:

![14-predict-us](https://user-images.githubusercontent.com/7065401/110488598-62d96f00-80cd-11eb-828f-d3ebf0190e51.png)
> Predicted cases in the US


## Final thoughts

Our objective with this post is to help you understand the process followed by Data Scientists and the structure of a real Data Science project, regarding a very real, current situation.

We can say that, unlike our [first analysis](https://blog.rmotr.com/learn-data-science-by-analyzing-covid-19-27a063d7f442), now **reality is behaving better than our predictions**. What our model infers outweigh what is actually happening, COVID seems to be retreating and one possible cause could be the rising of the vaccination.

Is the epidemic finally coming to an end? possibly, but we still need to stay safe, sharp and help each other.

Hopefully, we’ll soon look back at this analysis and confirm that our predictions were extremely off and COVID-19 has immensely slowed down. Even better, it remains a memory, or a demo Data Science project.

Thank you for reading.

