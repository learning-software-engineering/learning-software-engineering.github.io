# **Requirements.txt**

## **Introduction**


`requirements.txt` is a crucial file in Python projects for managing dependencies. It lists all the packages required to run your project, including their specific versions. This file ensures consistency and simplifies the setup process for other developers working on the project.


## **How to use?**

### **Creating a requirements.txt file**

To create and update a `requirements.txt` file, use the following command in your terminal:

```bash
pip freeze > requirements.txt
```

This command generates a list of all installed packages and their versions in your virtual environment and saves them to a `requirements.txt` file.


### **Installing dependencies from a requirements.txt file**

To install the dependencies listed in a `requirements.txt` file, use the following command in your terminal:

```bash
pip install -r requirements.txt
```

This command reads the packages and their versions from the **`requirements.txt`** file and installs them in your virtual environment.

**Resources:**
- [How to Create and Maintain a requirements.txt](https://learnpython.com/blog/python-requirements-file/)



## **Best Practices**

1. **Use a virtual environment:** Always work within a virtual environment to isolate your project's dependencies from your system's global Python environment.
    
    [Guide to Python Virtual Environments](https://www.dataquest.io/blog/a-complete-guide-to-python-virtual-environments/)
    
1. **Keep the file up-to-date:** Regularly update the `requirements.txt` file as you add, remove, or update dependencies.
2. **List only necessary dependencies:** Only list the Python modules and packages your project needs. Do not include unnecessary modules or packages, as this makes the txt file bloated and difficult to read. It is also a waste of resources.

**More Best Practices:**
- [10 Python Requirements.txt Best Practices](https://climbtheladder.com/10-python-requirements-txt-best-practices/)
