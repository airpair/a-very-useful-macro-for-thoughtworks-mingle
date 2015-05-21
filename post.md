### What is [Mingle](http://www.thoughtworks.com/mingle/)?

Mingle is a to-do tracker unlike any other. It is customizable beyond your wildest dreams. If you need more than "New", "In progress", "Completed" - you can add new sections via the interface. It seems like literally every part of the site can be modified or removed. At times, the level of customization can be a bit much, but if you read a good tutorial you'll understand and appreciate the complexity.

### What is [Mingle Query Language](http://www.thoughtworks.com/mingle/docs/macro_and_mql_guide.html)?

Mingle Query Language is the built in solution that is more or less SQL. Looking at the syntax, you'll barely notice the difference. You can use it to generate some great reports - but there is a barrier to entry - that I am going to break down for you.

### Let's make that Macro

![picture add item](https://raw.githubusercontent.com/juliusakula/mingle-tutorial/master/images/add%20item.png)

> Our goal: Create a chart that shows who on the team has the most work to do.

1. [Get an account](http://www.thoughtworks.com/mingle/pricing/) on mingle **(free for less than 5 users)**
2. Populate your project with some cards.

**I created a new mingle account for the purpose of this tutorial so that you could follow along** if you are starting from scratch. For the macro we are about to make, we need to have multiple items each with time estimates, and across at least 2 owners. 

Create a new Agile project - Mingle uses WalkMe as its tutorial engine. If you don't know how to create an Agile Project in Mingle, click that blue 'Walk Me Through' button at the bottom. Then click 'How to create a new Agile Project', the app will show you how to do that. It's important we start with an agile project, because the cards will by default have the attribute 'Estimate'. You can edit the card attributes in the project admin section, and if you want to do that I suggest you consult the [documentation](http://www.thoughtworks.com/mingle/docs/mingle_api.html).

Now that you have an Agile project, go to the Card Wall - we are going to make a few edits to 'Story 1', 'Story 2', and 'Story 3'. 

* For the Story 1 card, set the Owner to `(current user)`, and set the Estimate to `2`.
* For the Story 2 card, set the Owner to `(not set)` and set the Estimate to `4`.
* For the Story 3 card, set the Owner to `(current user)` and set the Estimate to `2`.

Ok, now we have enough data to create the macro.

### A macro card is a card that gets data from other cards

Create a new card, and then add a Stack Bar Chart by pushing this button.

![picture insert stack bar](https://raw.githubusercontent.com/juliusakula/mingle-tutorial/master/images/insert%20stack%20bar.png)

First you must fill out the chart level options:

* Set the condition to `estimate > 0` - this essentially selects items with any time estimate selected.
* Set cumulative to false
* Set the labels to `SELECT DISTINCT owner`

![chart level options](https://raw.githubusercontent.com/juliusakula/mingle-tutorial/master/images/chart%20level%20options.png)

Next are "Series Level Options" - these are individual queries that will return data to be plotted. Each section is stacked on top of each other. For the first series option:

* Set the data to `SELECT owner, sum(estimate) WHERE status = 'New'`
* Set the label to `Not Done`

![picture series level 1](https://raw.githubusercontent.com/juliusakula/mingle-tutorial/master/images/series%20level%20options1.png)

For the second series option:

* Set the data to `SELECT owner, sum(estimate) WHERE status = 'Done'`
* Set the label to `Done`

![picture series level 2](https://raw.githubusercontent.com/juliusakula/mingle-tutorial/master/images/series%20level%20options2.png)

Now you  can click preview, and see your chart!

![picture chart preview](https://raw.githubusercontent.com/juliusakula/mingle-tutorial/master/images/final%20chart.png)

Mingle is very cool but also very complicated. They know their target demographic is programmers, so there is a certain expectation you can figure these things out. The Mingle Query Language syntactically resembles SQL so much that with basic knowledge of SQL, I did not have to look up a single thing, but it took me a minute to create an analogy between SQL's Databases->Tables->Columns and MQL's structure.

Think of MQL as having a single Database or Schema and a single Table. The columns are always card attributes. There are never FROM clauses, because of the fact there is only a single table. For more information, consult the [MQL Syntax section](http://www.thoughtworks.com/mingle/docs/mql_reference.html) of the documentation.

With the amount of functionality that is provided, I don't think that they could make it any simpler. Using mingle in your workflow will be less complicated - when you are done setting up macros and reports you typically don't have to create more. Setting up the macros is a one-off technical investment, but can help you visualize your team's workload. The typical workflow involving to-do items has nothing to do with macros, so if you simply want to track your tasks, check out mingle - the day to day workflow is simpler than this - this was the most complicated thing I could think of within Mingle to write a tutorial for. Check [Mingle](http://www.thoughtworks.com/mingle/) out for yourself!