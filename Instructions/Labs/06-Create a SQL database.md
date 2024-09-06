# Lab 06 - Create a SQL database

## Lab overview

A SQL database is a collection of tables that stores a specific set of structured data using a relational model. It is designed to efficiently organize and retrieve data using a language called Structured Query Language (SQL).

In this walkthrough, we will create a SQL database in Azure and then query the data in that database.

## Lab objectives

In this lab, you will complete the following tasks:

+ Task 1: Create the database
+ Task 2: Test the database

## Estimated timing: 20 minutes

## Architecture diagram

![](../images/az900lab06.PNG) 

### Task 1: Create the database

In this task, we will create a SQL database based on the AdventureWorksLT sample database. 

1. On the Azure portal, from the **Search resources, services, and docs** blade, search for and select **SQL databases**, and then click **+ Create**. 

1. On the **Basics** tab, fill in this information.  

    | Setting | Value | 
    | --- | --- |
    | Subscription | **Choose your subscription** |
    | Resource group | **myRGDb-<inject key="DeploymentID" enableCopy="false"/>** |
    | Database name| **db1** |
    | Workload Environment| **Development** |
    
1. Next to the **Server** drop down list, click **Create new**. Click **OK** when finished.          

    | Setting | Value | 
    | --- | --- |
    | Server name | **sqlserver<inject key="DeploymentID" enableCopy="false"/>** (must be unique) |
    | Location | **(US) East US** |
    | Authentication method | **Use SQL authentication** | 
    | Server admin login | **sqluser** |
    | Password | **Pa$$w0rd1234** |
    | Confirm Password | **Pa$$w0rd1234** |

1. Back on Basics tab then specify the following:

   | Setting | Value | 
   | --- | --- |
   | Compute + storage| **General Purpose - Serverless Gen 5** |

   >**Note**: If Serverless is not select kindly click on **Configure database** > in **Compute tier** choose **Serverless**.

1. Select **Next: Networking >** tab and configure the following settings (leave others with their defaults) 

    | Setting | Value | 
    | --- | --- |
    | Connectivity method | **Public endpoint** |    
    | Allow Azure services and resources to access this server | **Yes** |
    | Add current client IP address | **No** |

1. Select **Next: Security >**. On the **Security** tab.
 
    | Setting | Value | 
    | --- | --- |
    | Enable Microsoft Defender for SQL| **Not now** |

1. Select **Next: Additional settings >**. We will be using the AdventureWorksLT sample database, if pop-up comes, click on **OK**.

    | Setting | Value | 
    | --- | --- |
    | Use existing data | **Sample** |

1. Click **Review + create (2)**, review the configurations, and then click **Create** to deploy and provision the resource group, server, and database. Deployment may take approximately 2 to 5 minutes.

    ![Screenshot of the Additional settings tab of the Create SQL Database blade with settings selected as per the table and the Review + create button highlighted.](../images/lab6nj.png)

1. Wait for the deployment to get succeeded.

### Task 2: Test the database

In this task, we will configure the SQL server and run a SQL query. 

1. From the **Search resources, services, and docs** blade, search and select **SQL databases** and ensure your new database was created. You may need to **Refresh** the page.

    ![Screenshot of the SQL database and server that have just been deployed.](../images/db1.png)

1. Click the **db1** entry representing the SQL database you created, and then click **Query editor (preview)** from the left navigation pane.

1. Login as **sqluser** with the password **Pa$$w0rd1234**, and click on **OK**.

1.  If you are not able to login, follow the below steps: 

    ![Screenshot of the Query Editor login page with IP address error.](../images/0503.png)
    
    >**Note:** If you are able to login proceed with step 9.

1. From the **db1** blade, click **Overview**. 

1. From the SQL server **Overview** blade, click **Set server firewall**.

1. Scroll down to the Firewall rules section and click on **+ Add your client IPv4 address**. Be sure to **Save** your changes. 

    ![Screenshot of the SQL server firewall settings page with the new IP rule highlighted.](../images/az-900mod-6img-2.png)

1. Return to your SQL database and the **Query Editor (Preview)** login page. Try to login again as **sqluser** with the password **Pa$$w0rd1234**. Click on **OK**. This time you should succeed. Note that it may take a couple of minutes for the new firewall rule to be deployed. 

1. Once you log in successfully the query pane appears, enter the following query into the editor pane.

    ```
    SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
    FROM SalesLT.ProductCategory pc
    JOIN SalesLT.Product p
    ON pc.productcategoryid = p.productcategoryid;
    ```

    ![Screenshot of the Query editor with the query pane and the commands executing successfully.](../images/0507.png)

    >**Note**: This SQL query selects the top 20 records from the SalesLT.ProductCategory table and SalesLT.Product table, displaying the CategoryName from the ProductCategory table as "CategoryName" and the ProductName from the Product table as "ProductName." The query performs an inner join between the two tables based on the productcategoryid column

1. Click **Run**, and then review the query results in the **Results** pane. The query should run successfully.

    ![Screenshot of the database Query Editor pane with the SQL code having been run successfully and the output visible in the results pane.](../images/0508.png)

<validation step="75515f24-70f3-4cf2-9172-0dcd50b3f807" />

> **Congratulations** on completing the task! Now, it's time to validate it.

### Review
In this lab, you have completed:
- Created the database
- Tested the database

## Reference link

- https://learn.microsoft.com/en-us/sql/relational-databases/databases/create-a-database?view=sql-server-ver16
  
## You have successfully completed this lab.
