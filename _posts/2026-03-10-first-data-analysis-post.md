---
title: "Python Basics for Data Analysis: My First Notebooks"
date: 2026-03-10
categories: [data-analysis]
---

This article explores setting up a simple introductory data analysis learning environment and how to use it. 

<h2>Introduction</h2>

The field of data analysis has a wide variety of tools and learning platforms to choose from. While some of these tools have specific features in common, many of them also have unique features or characteristics. For a learner new to data analysis, it can be overwhelming to pick a starting point and choose which tools to learn first.

The goal of this article is to share the plan I created for setting up my data analysis learning environments and becomming familiar with basic tools so that others can follow along as well. However, it is important to note that individual discretion must be applied as not all tools and/or platforms may be suitable for an individual's specific project or learning goals.

<h2>Tools Used</h2>

- [Python](https://www.python.org/downloads/)

- [Jupyter](https://jupyter.org/install)

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

- [Power BI Desktop](https://www.microsoft.com/en-us/download/details.aspx?id=58494)

- [pandas](https://pandas.pydata.org/docs/getting_started/index.html)

<h2>Process</h2>

1. Install Python.

2. Install Git and set up [GitHub repo](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories) for storing projects.

3. Install Power BI Desktop.

4. Test first Python script: `hello_world.py`.

    4.1. It may be useful for first-time learners to follow a [tutorial](https://www.w3schools.com/python/python_getstarted.asp) for writing and running python scripts.

5. Set up Python virtual environment for running Jupyter Notebook.

    5.1. Inside your project directory, create the virtual environment (`myvenv`):

    ```bash
    python3 -m venv myvenv
    ```

    5.2. Activate the virtual environment:

    ```bash
    source myvenv/bin/activate
    ```

    5.3. Install required packagages. This will vary depending on the project, but the example below shows the required packages that are needed for the pandas [getting started](https://pandas.pydata.org/docs/getting_started/intro_tutorials/02_read_write.html) tutorial:

    If creating your own environment:
        
    ```bash
    pip install pandas jupyter ipykernel
    ```

    Then, to create a `requirements.txt` file that can be used to easily install all the necessary dependencies for your project again in another environment later on: 

    ```bash
    pip freeze > requirements.txt
    ```

    Note: make sure to do this every time you add/change the dependencies for your project.

    If creating an environment using a clone of a project repo that contains a `requirements.txt` file with the dependencies needed:

    ```bash
    pip install -r requirements.txt
    ```

    5.4. Register the kernel for Jupyter:

    ```bash
    python3 -m ipykernel install --user --name=myvenv --display-name "Python (myvenv)"
    ```

6. Explore pandas basics: read CSV, head(), info()

    6.1. Create a [Jupyter notebook](https://www.dataquest.io/blog/jupyter-notebook-tutorial/).

    6.2. Set up the notebook to explore pandas features. It may be useful to follow the pandas [getting started](https://pandas.pydata.org/docs/getting_started/intro_tutorials/02_read_write.html) tutorial. 

    6.3. Run the notebook cells to see the pandas outputs.

7. Load sample dataset into Power BI.

    7.1. Power BI comes with some sample datasets such as the one called `financials`, which can be loaded by following the [create a report](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-excel-stunning-report) tutorial.

<h2>Challenges & Lessons Learned</h2>

- Run first `hello_world.py` Python script:

    - To run the script, in the terminal, type: 

        ```bash
        python3 hello_world.py
        ```

    - Note: on some systems it may be necessary to instead type: 

        ```bash
        python hello_world.py
        ```

- Creating a Python virtual environment to run Jupyter Notebooks is a recommended best practice to avoid conflicts that may result from the dependencies that your individual projects use.

- Run first Jupyter notebook:

    1. Start Jupyter in project folder (make sure `myvenv` is active first - see step 5.2.):

        ```bash
        jupyter notebook
        ```

    2. Open notebook in [browser](http://localhost:8888) (alternatively, if using VSCode extension, the notebook can be run directly from the IDE instead of a browser).

    3. Change the kernel to the one you named in step 5.4.

    4. Run the cells sequentially to see the outputs.

    5. Note: to stop the virtual environment when done, type:

        ```bash
        deactivate
        ```

- Explore pandas features:

    - `read_csv()`: reads data from a CSV file into a DataFrame object. 

    - `head()`: outputs the first few rows from the CSV file. 

    - `info()`: outputs technical information about the DataFrame object such as number of columns, number of non-null values, etc.

- Load sample dataset into Power BI:

    1. Prepare imported data: format data types, headings, filter data, etc.

    2. Write expressions if necessary. 

    3. Enter table view mode to confirm data was imported successfully. The name of the dataset will appear in the pane on the right side of the screen.

<h2>Screenshots / Diagrams</h2>

Successfully loading the sample dataset `financials` into Power BI will look similar to the image below:

![Loaded Data](/images/data_loaded.PNG)

Exploring the pandas feature `df.head()` on the `titanic.csv` file from the tutorial will produce output that looks similar to the image below: 

![Pandas Tutorial](/images/pandas_tutorial_dfhead.png)

<h2>Next Steps</h2>

- Practice more Python basics (variables, loops, functions).

- Practice loading and cleaning datasets from Kaggle in Power BI and Jupyter notebooks.

- Learn how to handle missing values in datasets with pandas.

- Learn how to create simple visuals such as bar charts in Power BI.

- Learn how to use matplotlib and Seaborn.