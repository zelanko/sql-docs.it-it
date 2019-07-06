---
title: Il passaggio di parametri agli updategram (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 45c6f1d61df8f3f83b1cb8f579535882a9c1ad98
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67584672"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>Passaggio di parametri agli updategram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Gli updategram sono modelli e in quanto tali è possibile passare loro parametri. Per altre informazioni sul passaggio di parametri ai modelli, vedere [considerazioni sulla sicurezza degli Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md).  
  
 Gli updategram consentono di passare NULL come valore di parametro. Per passare il valore di parametro NULL, si specifica la **nullvalue** attributo. Il valore assegnato per il **nullvalue** attributo viene quindi specificato come valore del parametro. e considerato come NULL dagli updategram.  
  
> [!NOTE]  
>  Nelle  **\<SQL: header >** e  **\<updg:header >** , è necessario specificare il **nullvalue** come non qualificato, mentre nella  **\<updg: Sync >** , si specifica il **nullvalue** come qualificato (ad esempio **updg: NullValue**).  
  
## <a name="examples"></a>Esempi  
 Per creare esempi reali utilizzando gli esempi seguenti, è necessario soddisfare i requisiti specificati nelle [requisiti per l'esecuzione di esempi di SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Prima di utilizzare gli esempi dell'updategram, si tenga presente quanto segue:  
  
-   Negli esempi viene utilizzato il mapping predefinito, ovvero non viene specificato alcuno schema di mapping nell'updategram. Per altri esempi di updategram che utilizzano schemi di mapping, vedere [specifica uno Schema di Mapping con annotazioni in un Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. Passaggio di parametri a un updategram  
 In questo esempio l'updategram modifica il cognome di un dipendente nella tabella HumanResources.Shift. L'updategram verrà passato due parametri: ShiftID, utilizzato in modo univoco un turno e assegnare un nome.  
  
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
  
2.  Preparare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) in [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) per eseguire l'updategram aggiungendo le righe seguenti dopo la `cmd.Properties("Output Stream").Value = outStream`:  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

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
  
2.  Preparare lo script di test SQLXML 4.0 (Sqlxml4test.vbs) in [utilizzo di ADO per eseguire query di SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) per eseguire l'updategram aggiungendo le righe seguenti dopo la `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza degli updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
