---
title: Applicazione di esempio (driver PDO_SQLSRV) | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a153e4ce-992d-4211-9a0f-c0998c706402
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8414497fed891e153399febf84151c82d915d77a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993594"
---
# <a name="example-application-pdosqlsrv-driver"></a>Applicazione di esempio (driver PDO_SQLSRV)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

L'applicazione di esempio AdventureWorks Product Reviews è un'applicazione Web che usa il driver PDO_SQLSRV dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. L'applicazione consente agli utenti di cercare i prodotti immettendo una parola chiave, visualizzare i commenti, scrivere una recensione e caricare un'immagine per un prodotto selezionato.  
  
### <a name="running-the-example-application"></a>Esecuzione dell'applicazione di esempio  
  
1.  Installare i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Per informazioni dettagliate, vedere [Introduzione con i driver Microsoft per php per SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)
2.  Copiare il codice indicato più avanti in questo documento in due file: adventureworks_demo.php e photo.php.  
3.  Inserire i file adventureworks_demo.php e photo.php nella directory radice del server Web.  
4.  Eseguire l'applicazione avviando https\://localhost/adventureworks_demo.php dal browser.  
  
## <a name="requirements"></a>Requisiti  
Per eseguire l'applicazione di esempio AdventureWorks Product Reviews, è necessario che il computer soddisfi i seguenti requisiti:  
  
-   Il sistema soddisfa i requisiti per i [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Per informazioni dettagliate, vedere [requisiti di sistema per i driver Microsoft per php per SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md).  
 -   I file adventureworks_demo.php e photo.php si trovano nella directory radice del server Web. I file devono contenere il codice riportato più avanti in questo documento.  
-   SQL Server 2005 o SQL Server 2008 con il database [AdventureWorks2008](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) associato deve essere installato nel computer locale.  
-   Un browser Web installato.  
  
## <a name="demonstrates"></a>Dimostrazione  
L'applicazione di esempio AdventureWorks Product Reviews descrive come:  
  
-   Aprire una connessione a SQL Server usando l'autenticazione di Windows.  
-   Preparazione ed esecuzione di una query con parametri.  
-   Come recuperare i dati.  
-   Verificare la presenza di errori.  
  
## <a name="example"></a>Esempio  
L'applicazione di esempio AdventureWorks Product Reviews restituisce le informazioni del database relative ai prodotti i cui nomi contengono una stringa immessa dall'utente. Dall'elenco dei prodotti restituiti, l'utente può visualizzare le recensioni, visualizzare un'immagine, caricare un'immagine e scrivere una recensione per un prodotto selezionato.  
  
Inserire il codice seguente in un file denominato adventureworks_demo_pdo.php:  
  
```  
<!--=============  
This file is part of a Microsoft SQL Server Shared Source Application.  
Copyright (C) Microsoft Corporation.  All rights reserved.  
  
THIS CODE AND INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY  
KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE  
IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A  
PARTICULAR PURPOSE.  
============= *-->  
  
<!--Note: The presentation formatting of this example application -->  
<!-- is intentionally simple to emphasize the SQL Server -->  
<!-- data access code.-->  
<html>  
<head>  
<title>AdventureWorks Product Reviews</title>  
</head>  
<body>  
<h1 align='center'>AdventureWorks Product Reviews</h1>  
<h5 align='center'>This application is a demonstration of the   
                   object oriented API (PDO_SQLSRV driver) for the   
                   Microsoft Drivers for PHP for SQL Server.</h5><br/>  
<?php  
$serverName = "(local)\sqlexpress";  
  
/* Connect using Windows Authentication. */  
try  
{  
$conn = new PDO( "sqlsrv:server=$serverName ; Database=AdventureWorks", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
catch(Exception $e)  
{   
die( print_r( $e->getMessage() ) );   
}  
  
if(isset($_REQUEST['action']))  
{  
switch( $_REQUEST['action'] )  
{  
/* Get AdventureWorks products by querying against the product name.*/  
case 'getproducts':  
try  
{  
$params = array($_POST['query']);  
$tsql = "SELECT ProductID, Name, Color, Size, ListPrice   
 FROM Production.Product   
 WHERE Name LIKE '%' + ? + '%' AND ListPrice > 0.0";  
  
$getProducts = $conn->prepare($tsql);  
$getProducts->execute($params);  
$products = $getProducts->fetchAll(PDO::FETCH_ASSOC);  
$productCount = count($products);  
if($productCount > 0)  
{  
BeginProductsTable($productCount);  
foreach( $products as $row )  
{  
PopulateProductsTable( $row );  
}  
EndProductsTable();  
}  
else  
{  
DisplayNoProdutsMsg();  
}  
}  
catch(Exception $e)  
{   
die( print_r( $e->getMessage() ) );   
}  
GetSearchTerms( !null );  
break;  
  
/* Get reviews for a specified productID. */  
case 'getreview':  
GetPicture( $_GET['productid'] );  
GetReviews( $conn, $_GET['productid'] );  
break;  
  
/* Write a review for a specified productID. */  
case 'writereview':  
DisplayWriteReviewForm( $_POST['productid'] );  
break;  
  
/* Submit a review to the database. */  
case 'submitreview':  
try  
{  
$tsql = "INSERT INTO Production.ProductReview (ProductID,   
   ReviewerName,   
   ReviewDate,   
   EmailAddress,   
   Rating,   
   Comments)   
        VALUES (?,?,?,?,?,?)";  
$params = array(&$_POST['productid'],   
&$_POST['name'],   
date("Y-m-d"),   
&$_POST['email'],   
&$_POST['rating'],   
&$_POST['comments']);  
$insertReview = $conn->prepare($tsql);  
$insertReview->execute($params);  
}  
catch(Exception $e)  
{   
die( print_r( $e->getMessage() ) );   
}  
GetSearchTerms( true );  
GetReviews( $conn, $_POST['productid'] );  
break;  
  
/* Display form for uploading a picture.*/  
case 'displayuploadpictureform':  
try  
{  
$tsql = "SELECT Name FROM Production.Product WHERE ProductID = ?";  
$getName = $conn->prepare($tsql);  
$getName->execute(array($_GET['productid']));  
$name = $getName->fetchColumn(0);  
}  
catch(Exception $e)  
{   
die( print_r( $e->getMessage() ) );   
}  
DisplayUploadPictureForm( $_GET['productid'], $name );  
break;  
  
/* Upload a new picture for the selected product. */  
case 'uploadpicture':           
try  
{  
$tsql = "INSERT INTO Production.ProductPhoto (LargePhoto)   
 VALUES (?)";  
$uploadPic = $conn->prepare($tsql);  
$fileStream = fopen($_FILES['file']['tmp_name'], "r");  
$uploadPic->bindParam(1,    
  $fileStream,   
  PDO::PARAM_LOB,   
  0,   
  PDO::SQLSRV_ENCODING_BINARY);  
$uploadPic->execute();  
  
/* Get the first field - the identity from INSERT -   
   so we can associate it with the product ID. */  
$photoID = $conn->lastInsertId();  
$tsql = "UPDATE Production.ProductProductPhoto   
 SET ProductPhotoID = ?   
 WHERE ProductID = ?";  
$associateIds = $conn->prepare($tsql);  
$associateIds->execute(array($photoID, $_POST['productid']));  
}  
catch(Exception $e)  
{  
die(print_r($e->getMessage()));  
}  
  
GetPicture( $_POST['productid']);  
DisplayWriteReviewButton( $_POST['productid'] );  
GetSearchTerms (!null);  
break;  
}//End Switch  
}  
else  
{  
    GetSearchTerms( !null );  
}  
  
function GetPicture( $productID )  
{  
    echo "<table align='center'><tr align='center'><td>";  
    echo "<img src='photo_pdo.php?productId=".$productID."'   
      height='150' width='150'/></td></tr>";  
    echo "<tr align='center'><td><a href='?action=displayuploadpictureform&productid=".$productID."'>Upload new picture.</a></td></tr>";  
    echo "</td></tr></table></br>";  
}  
  
function GetReviews( $conn, $productID )  
{  
try  
{  
$tsql = "SELECT ReviewerName,   
CONVERT(varchar(32),   
ReviewDate, 107) AS [ReviewDate],   
Rating,   
Comments   
 FROM Production.ProductReview   
 WHERE ProductID = ?   
 ORDER BY ReviewDate DESC";  
$getReviews = $conn->prepare( $tsql);  
$getReviews->execute(array($productID));  
$reviews = $getReviews->fetchAll(PDO::FETCH_NUM);  
$reviewCount = count($reviews);  
if($reviewCount > 0 )  
{  
foreach($reviews as $row)  
{  
$name = $row[0];  
$date = $row[1];  
$rating = $row[2];  
$comments = $row[3];  
DisplayReview( $productID, $name, $date, $rating, $comments );  
}  
}  
else  
{  
DisplayNoReviewsMsg();   
}  
}  
catch(Exception $e)  
{  
die(print_r($e->getMessage()));  
}  
    DisplayWriteReviewButton( $productID );  
GetSearchTerms(!null);  
}  
  
/*** Presentation and Utility Functions ***/  
  
function BeginProductsTable($rowCount)  
{  
    /* Display the beginning of the search results table. */  
$headings = array("Product ID", "Product Name", "Color", "Size", "Price");  
echo "<table align='center' cellpadding='5'>";   
echo "<tr bgcolor='silver'>$rowCount Results</tr><tr>";  
foreach ( $headings as $heading )  
{  
echo "<td>$heading</td>";  
}  
echo "</tr>";  
}  
  
function DisplayNoProdutsMsg()  
{  
    echo "<h4 align='center'>No products found.</h4>";  
}  
  
function DisplayNoReviewsMsg()  
{  
    echo "<h4 align='center'>There are no reviews for this product.</h4>";  
}  
  
function DisplayReview( $productID, $name, $date, $rating, $comments)  
{  
    /* Display a product review. */  
    echo "<table style='WORD-BREAK:BREAK-ALL' width='50%' align='center' border='1' cellpadding='5'>";   
    echo "<tr>  
            <td>ProductID</td>  
            <td>Reviewer</td>  
            <td>Date</td>  
            <td>Rating</td>  
          </tr>";  
      echo "<tr>  
              <td>$productID</td>  
              <td>$name</td>  
              <td>$date</td>  
              <td>$rating</td>  
            </tr>  
            <tr>  
              <td width='50%' colspan='4'>$comments</td></tr></table><br/><br/>";  
}  
  
function DisplayUploadPictureForm( $productID, $name )  
{  
    echo "<h3 align='center'>Upload Picture</h3>";  
    echo "<h4 align='center'>$name</h4>";  
    echo "<form align='center' action='adventureworks_demo_pdo.php'   
enctype='multipart/form-data' method='POST'>  
<input type='hidden' name='action' value='uploadpicture'/>  
<input type='hidden' name='productid' value='$productID'/>  
<table align='center'>  
 <tr>  
   <td align='center'>  
 <input id='fileName' type='file' name='file'/>  
   </td>  
 </tr>  
 <tr>  
   <td align='center'>  
<input type='submit' name='submit' value='Upload Picture'/>  
   </td>  
 </tr>  
</table>  
  </form>";  
}  
  
function DisplayWriteReviewButton( $productID )  
{  
    echo "<table align='center'><form action='adventureworks_demo_pdo.php'   
             enctype='multipart/form-data' method='POST'>  
          <input type='hidden' name='action' value='writereview'/>  
          <input type='hidden' name='productid' value='$productID'/>  
          <input type='submit' name='submit' value='Write a Review'/>  
          </p></td></tr></form></table>";  
}  
  
function DisplayWriteReviewForm( $productID )  
{  
    /* Display the form for entering a product review. */  
    echo "<h5 align='center'>Name, E-mail, and Rating are required fields.</h5>";  
    echo "<table align='center'>  
<form action='adventureworks_demo_pdo.php'   
  enctype='multipart/form-data' method='POST'>  
<input type='hidden' name='action' value='submitreview'/>  
<input type='hidden' name='productid' value='$productID'/>  
<tr>  
<td colspan='5'>Name: <input type='text' name='name' size='50'/></td>  
</tr>  
<tr>  
<td colspan='5'>E-mail: <input type='text' name='email' size='50'/></td>  
</tr>  
<tr>  
<td>Rating: 1<input type='radio' name='rating' value='1'/></td>  
<td>2<input type='radio' name='rating' value='2'/></td>  
<td>3<input type='radio' name='rating' value='3'/></td>  
<td>4<input type='radio' name='rating' value='4'/></td>  
<td>5<input type='radio' name='rating' value='5'/></td>  
</tr>  
<tr>  
<td colspan='5'>  
<textarea rows='20' cols ='50' name='comments'>[Write comments here.]</textarea>  
</td>  
</tr>  
<tr>  
<td colspan='5'>  
<p align='center'><input type='submit' name='submit' value='Submit Review'/>  
</td>  
</tr>  
</form>  
          </table>";  
}  
  
function EndProductsTable()  
{   
    echo "</table><br/>";   
}  
  
function GetSearchTerms( $success )  
{  
    /* Get and submit terms for searching the database. */  
    if (is_null( $success ))  
    {  
echo "<h4 align='center'>Review successfully submitted.</h4>";}  
echo "<h4 align='center'>Enter search terms to find products.</h4>";  
echo "<table align='center'>  
<form action='adventureworks_demo_pdo.php'   
  enctype='multipart/form-data' method='POST'>  
<input type='hidden' name='action' value='getproducts'/>  
<tr>  
   <td><input type='text' name='query' size='40'/></td>  
</tr>  
<tr align='center'>  
   <td><input type='submit' name='submit' value='Search'/></td>  
</tr>  
</form>  
  </table>";  
}  
  
function PopulateProductsTable( $values )  
{  
    /* Populate Products table with search results. */  
    $productID = $values['ProductID'];  
    echo "<tr>";  
    foreach ( $values as $key => $value )  
    {  
        if ( 0 == strcasecmp( "Name", $key ) )  
        {  
            echo "<td><a href='?action=getreview&productid=$productID'>$value</a></td>";  
        }  
        elseif( !is_null( $value ) )  
        {  
            if ( 0 == strcasecmp( "ListPrice", $key ) )  
            {  
                /* Format with two digits of precision. */  
                $formattedPrice = sprintf("%.2f", $value);  
                echo "<td>$$formattedPrice</td>";  
            }  
            else  
            {  
                echo "<td>$value</td>";  
            }  
        }  
        else  
        {  
            echo "<td>N/A</td>";  
        }  
    }  
    echo "<td>  
            <form action='adventureworks_demo_pdo.php' enctype='multipart/form-data' method='POST'>  
            <input type='hidden' name='action' value='writereview'/>  
            <input type='hidden' name='productid' value='$productID'/>  
            <input type='submit' name='submit' value='Write a Review'/>  
            </td></tr>  
            </form></td></tr>";  
}  
?>  
</body>  
</html>  
```  
  
## <a name="example"></a>Esempio  
Lo script photo.php restituisce la foto del **ProductID**specificato. Questo script viene chiamato dallo script adventureworks_demo.php.  
  
Inserire il codice seguente in un file denominato photo_pdo.php:  
  
```  
<?php  
/*  
=============  
This file is part of a Microsoft SQL Server Shared Source Application.  
Copyright (C) Microsoft Corporation.  All rights reserved.  
  
THIS CODE AND INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY  
KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE  
IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A  
PARTICULAR PURPOSE.  
=============  
*/  
$serverName = "(local)\sqlexpress";  
  
/* Connect using Windows Authentication. */  
try  
{  
$conn = new PDO( "sqlsrv:server=$serverName ; Database=AdventureWorks", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
catch(Exception $e)  
{   
die( print_r( $e->getMessage() ) );   
}  
  
/* Get the product picture for a given product ID. */  
try  
{  
$tsql = "SELECT LargePhoto   
 FROM Production.ProductPhoto AS p  
 JOIN Production.ProductProductPhoto AS q  
 ON p.ProductPhotoID = q.ProductPhotoID  
 WHERE ProductID = ?";  
$stmt = $conn->prepare($tsql);  
$stmt->execute(array(&$_GET['productId']));  
$stmt->bindColumn(1, $image, PDO::PARAM_LOB, 0, PDO::SQLSRV_ENCODING_BINARY);  
$stmt->fetch(PDO::FETCH_BOUND);  
echo $image;  
}  
catch(Exception $e)  
{   
die( print_r( $e->getMessage() ) );   
}  
?>  
```  
  
## <a name="see-also"></a>Vedere anche  
[Connessione al server](../../connect/php/connecting-to-the-server.md)

[Confronto delle funzioni di esecuzione](../../connect/php/comparing-execution-functions.md)

[Recupero di dati](../../connect/php/retrieving-data.md)

[Aggiornamento dei dati &#40;Driver Microsoft per PHP per SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
