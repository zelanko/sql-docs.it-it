---
title: Mapping tra i tipi di dati nell'Importazione/Esportazione guidata SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 669be403-cb17-4b12-bbbf-e7a74003c4b6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3d8ff79cbcd5f243ef80c2be49bff7be78db4e20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114446"
---
# <a name="data-type-mapping-in-the-sql-server-import-and-export-wizard"></a>Mapping tra i tipi di dati nell'Importazione/Esportazione guidata SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 Nell'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile impostare il nome, il tipo di dati e le proprietà del tipo di dati delle colonne nei nuovi file e tabelle di destinazione, ma non è possibile specificare conversioni personalizzate per i valori di colonna. Il mapping dei tipi di dati dall'origine alla destinazione risulta quindi di primaria importanza.  
  
##  <a name="wizardMapping"></a> Come viene eseguito il mapping dei tipi di dati tra origine e destinazione durante la procedura guidata?
La procedura guidata usa file di mapping installati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per eseguire il mapping dei tipi di dati da un tipo o una versione di database a un altro. Ad esempio, può eseguire il mapping da tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tipi di dati Oracle. Per impostazione predefinita, i file di mapping in formato XML sono installati nelle cartelle seguenti.
-   **C:\Programmi\Microsoft SQL Server\130\DTSMappingFiles\\** (per 64 bit)
-   **C:\Programmi (x86)\Microsoft SQL Server\130\DTSMappingFiles\\** (per 32 bit)  
  
 Se si modifica un file di mapping esistente o si aggiunge un nuovo file di mapping alla cartella, è necessario chiudere e riaprire l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per caricare il file di mapping nuovo o modificato.  
 
## <a name="you-can-change-an-existing-mapping-file"></a>È possibile modificare un file di mapping esistente
Se sono necessari modelli di mapping diversi tra i tipi di dati, è possibile aggiornare i file di mapping per modificare i modelli di mapping usati dalla procedura guidata. Se ad esempio si vuole eseguire il mapping del tipo di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **nchar** al tipo di dati DB2 **GRAPHIC** anziché al tipo di dati DB2 **VARGRAPHIC** durante il trasferimento di dati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a DB2, è possibile modificare il mapping di **nchar** nel file di mapping **SqlClientToIBMDB2.xml** in modo da usare **GRAPHIC** anziché **VARGRAPHIC**.  
  
## <a name="you-can-add-a-new-mapping-file"></a>È possibile aggiungere un nuovo file di mapping
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installa i tipi di mapping tra le combinazioni di origine e destinazione più comuni. È comunque possibile aggiungere nuovi file di mapping alla directory **MappingFiles** per supportare anche altre combinazioni di origine e destinazione. I nuovi file di mapping devono essere conformi allo schema XSD pubblicato ed eseguire il mapping tra una combinazione univoca di origine e destinazione. Lo schema per i file di mapping, **DataTypeMapping.xsd**, è disponibile [qui](https://schemas.microsoft.com/sqlserver/2008/07/IntegrationServices/DataTypeMapping/DataTypeMapping.xsd).
 
## <a name="sample-mapping-file"></a>Esempio di file di mapping
Di seguito è riportata una parte del file di mapping XML che esegue il mapping tra tipi di dati SQL Server (o, più precisamente, tra i tipi di dati usati dal provider di dati .Net Framework per SQL Server) e tipi di dati Oracle. Nell'esempio viene eseguito il mapping di un tipo di dati SQL Server **int** a un tipo di dati Oracle **INTEGER** .
  
```xml  
  
<dtm:DataTypeMappings  
    xmlns:dtm="https://www.microsoft.com/SqlServer/Dts/DataTypeMapping.xsd"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    SourceType="System.Data.SqlClient.SqlConnection"   
    MinSourceVersion="*"   
    MaxSourceVersion="*"   
    DestinationType="MSDAORA;OraOLEDB.Oracle;System.Data.OracleClient.OracleConnection"   
    MinDestinationVersion="08.*"   
    MaxDestinationVersion="*">  
  
    <!-- smallint -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>smallint</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
    <!-- int -->  
    <dtm:DataTypeMapping >  
        <dtm:SourceDataType>  
            <dtm:DataTypeName>int</dtm:DataTypeName>  
        </dtm:SourceDataType>  
        <dtm:DestinationDataType>  
            <dtm:SimpleType>  
                <dtm:DataTypeName>INTEGER</dtm:DataTypeName>  
            </dtm:SimpleType>  
        </dtm:DestinationDataType>  
    </dtm:DataTypeMapping>    
  
        ...  
  
</dtm:DataTypeMappings>  
  
```  

