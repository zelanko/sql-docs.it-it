---
title: Passaggio di parametri agli updategram (SQLXML)
description: Informazioni su come passare parametri agli updategram in SQLXML 4,0.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 129fceaeac7de8ca1ab44ff181dd0971b3744fa5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473102"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>Passaggio di parametri agli updategram (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Gli updategram sono modelli e in quanto tali è possibile passare loro parametri. Per ulteriori informazioni sul passaggio di parametri ai modelli, vedere [considerazioni sulla sicurezza degli Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md).  
  
 Gli updategram consentono di passare NULL come valore di parametro. Per passare il valore del parametro NULL, è necessario specificare l'attributo **NullValue** . Il valore assegnato all'attributo **NullValue** viene quindi fornito come valore del parametro. e considerato come NULL dagli updategram.  
  
> [!NOTE]  
>  In **\<sql:header>** e **\<updg:header>** , è necessario specificare la **NullValue** come non qualificata, mentre in **\<updg:sync>** si specifica **NullValue** come qualificato (ad esempio, **attributo updg: NullValue**).  
  
## <a name="examples"></a>Esempio  
 Per creare esempi funzionanti utilizzando gli esempi seguenti, è necessario soddisfare i requisiti specificati nei [requisiti per l'esecuzione di esempi SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Prima di utilizzare gli esempi dell'updategram, si tenga presente quanto segue:  
  
-   Negli esempi viene utilizzato il mapping predefinito, ovvero non viene specificato alcuno schema di mapping nell'updategram. Per ulteriori esempi di updategram che utilizzano schemi di mapping, vedere [specifica di uno schema di mapping con annotazioni in un Updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="a-passing-parameters-to-an-updategram"></a>R. Passaggio di parametri a un updategram  
 In questo esempio l'updategram modifica il cognome di un dipendente nella tabella HumanResources.Shift. All'updategram vengono passati due parametri: ShiftID, utilizzato per identificare in modo univoco un turno, e Name.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare l'updategram sopra indicato in Blocco note e salvarlo in un file con il nome UpdategramWithParameters.xml.  
  
2.  Preparare lo script di test SQLXML 4,0 (Sqlxml4test.vbs) nell' [utilizzo di ADO per eseguire query SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) per eseguire l'updategram aggiungendo le righe seguenti dopo `cmd.Properties("Output Stream").Value = outStream` :  

    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. Passaggio di NULL come valore di parametro a un updategram  
 Durante l'esecuzione di un updategram, il valore "isnull" viene assegnato al parametro che si desidera impostare su NULL. L'updategram converte il valore di parametro "isnull" in NULL e lo elabora di conseguenza.  
  
 Nell'updategram seguente la qualifica di un dipendente viene impostata su NULL:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Per testare l'updategram  
  
1.  Copiare l'updategram sopra indicato in Blocco note e salvarlo in un file con il nome UpdategramPassingNullvalues.xml.  
  
2.  Preparare lo script di test SQLXML 4,0 (Sqlxml4test.vbs) nell' [utilizzo di ADO per eseguire query SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) per eseguire l'updategram aggiungendo le righe seguenti dopo `cmd.Properties("Output Stream").Value = outStream` :  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
