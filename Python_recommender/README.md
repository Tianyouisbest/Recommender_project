This project is a recommender for an online retail company.

The project starts with the cleaned csv file, which is downloaded from professor Stirlin's git hub page. One of the important step when 
read this file is to make the 'InvoiceDate' column string instead of a "Timestamp" object. Because elastic search does not take the Timestamp object, and we are not using thie date in our project, it is best to just make it string. There are methods that can convert it back to date if needed, but that is not the goal of the project.

A bunch of useful functions for elastic search are created, like delete_es_index(index), execute_es_query(index, query). They will later be used to interact with elastic search. 

In the dataset, the 'InvoiceNo' is the column we use pandas to groupby, because we want to see which products are bought together in the same invoice, so that we can recommend a product in that invoice whenever another product in the same invoice are purchased. 

After some data transformation, the message we give elastic search will contain the following information:
InvoiceNo,
CustomerID,
InvoiceDate,
Country,
StockCodes,
Descriptions,
Quantities,
UnitPrices.
And then we aggregate based on matching stock codes. Each stock code indicate a type of product bought. This is how we identify 'customer who bought this also bought that'. The code will return the 'result', which contains the following:

The product bought in a particular invoice. 

The products bought along with the first product bought.

The information of the products bought along with the first product bought: their stock codes, doc_count, score, and bg_count. 

We can recommand the products that are bought together to other customers with this recommender, since their stock codes are extracted. 
