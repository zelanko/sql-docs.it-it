---
title: 'Modifica del formato di archiviazione per i tipi xs: DateTime, xs: date e xs: Time | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- xs:date
- xs:time
- storage format
- DateTime
ms.assetid: b9f758df-030c-4aec-8ade-1bf904aa2c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e8ccc6581e48a44e636fad07891bd8ec51596fbf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797643"
---
# <a name="changes-to-the-storage-format-for-types-xsdatetime-xsdate-and-xstime"></a>Modifiche al formato di archiviazione per i tipi xs:dateTime, xs:date e xs:time
  La regola XMLDATETIME identifica se i database contengono o meno dati XML tipizzati che non saranno più validi dopo l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Il formato di archiviazione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per i tipi xs: DateTime, xs: date e xs: Time è stato modificato per supportare valori con o senza informazioni sul fuso orario e consentire il mantenimento del fuso orario.  
  
 Se una raccolta XML Schema fa riferimento a uno di tali tipi, gli indici XML di tutte le colonne associate alla raccolta verranno disabilitati dopo l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Sarà possibile sottoporli a query utilizzando SELECT e/o XQUERIES, ma l'indice XML non verrà utilizzato. Se viene rilevato un valore di anno negativo, verrà generato un errore di runtime.  
  
 Inoltre, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non supporta valori con anni negativi.  
  
 La regola XMLDATETIME controlla se una raccolta XML Schema fa riferimento a uno dei tipi interessati e se esistono colonne XML tipizzate da tali raccolte.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Se la regola XMLDATETIME conferma che esistono colonne XML tipizzate in base a una raccolta di schemi che fa riferimento a xs:date, xs:time o xs:dateTime, è necessario rilevare innanzitutto se sono presenti o meno valori con anni negativi nei dati. La presenza di tali valori impedisce la ricompilazione degli indici XML dopo l'aggiornamento.  
  
 Con la query seguente vengono ricercate le raccolte di XML Schema che fanno riferimento ai tipi interessati e per tutte le colonne XML tipizzate. In questo modo è possibile stabilire se sono presenti o meno istanze con valori di anni negativi.  
  
```sql
CREATE PROCEDURE DateTimeInvestigation(@withdata bit)  
-- @withdata = 0: only get the affected meta data information  
-- @withdata = 1: get the affected meta data and instance information  
AS  
BEGIN  
-- First get XML containing all schema collections containing affected element and attributes  
-- components (model groups?)   
-- and columns that are affected by the schema collections.   
CREATE table #_dt_collector(x xml);   
;with dttypes as  
  (SELECT * FROM sys.xml_schema_components   
   where base_xml_component_id IN   
      (SELECT xml_component_id   
       FROM sys.xml_schema_types   
       where (name='dateTime' or name='date') and kind='P'  
      )   
   union all  
   SELECT * FROM sys.xml_schema_components  
   where xml_component_id IN   
      (SELECT xml_component_id   
       FROM sys.xml_schema_types   
       where (name='dateTime' or name='date') and kind='P'  
       or kind='N' or kind='Z')   
   ),   
dtplaced as  
  (SELECT scp.*   
   FROM sys.xml_schema_component_placements scp   
   JOIN dttypes on scp.placed_xml_component_id=dttypes.xml_component_id  
  )   
insert into #_dt_collector SELECT x FROM (SELECT  
  xsc.xml_collection_id as "@collid"  
, s.name as "@schema"  
, xscol.name as "@name"  
, count(xsc.xml_component_id) as "@affected_elems_and_attrs"  
, (SELECT S.Name as "@schema", T.Name as "@table"  
        , C.Name as "@column"   
   FROM sys.columns C   
   JOIN sys.tables T ON C.object_id = T.object_id  
   JOIN sys.schemas S ON S.schema_id = T.schema_id  
   WHERE C.xml_collection_id = xsc.xml_collection_id  
   FOR XML PATH('Columns'), TYPE  
  )   
FROM sys.xml_schema_components xsc  
JOIN dtplaced on xsc.xml_component_id=dtplaced.xml_component_id  
JOIN sys.xml_schema_collections xscol on xsc.xml_collection_id =xscol.xml_collection_id  
JOIN sys.schemas s on xscol.schema_id=s.schema_id  
group by xsc.xml_collection_id, s.name, xscol.name  
FOR XML PATH('XML_Schema_Collections'), TYPE) as T(x);   
if (@withdata = 0)    
  BEGIN  
  SELECT x as "*" FROM #_dt_collector for xml path(''), root('data');   
  drop table #_dt_collector;   
  return;   
  END;   
-- Declare cursor to find all columns bound to the schema collections  
DECLARE C CURSOR FOR  
SELECT S.Name, T.Name, C.Name   
FROM sys.columns C   
JOIN sys.tables T ON C.object_id = T.object_id  
JOIN sys.schemas S ON S.schema_id = T.schema_id  
WHERE C.xml_collection_id  
IN (SELECT distinct xsc.xml_collection_id  
    FROM sys.xml_schema_components xsc  
    JOIN (SELECT scp.*   
          FROM sys.xml_schema_component_placements scp   
          JOIN (SELECT * FROM sys.xml_schema_components   
                where base_xml_component_id    
                in (SELECT xml_component_id   
                    FROM sys.xml_schema_types   
                    where (name='dateTime' or name='date') and kind='P'  
                   )   
                union all  
                SELECT * FROM sys.xml_schema_components  
                where xml_component_id   
                in (SELECT xml_component_id   
                    FROM sys.xml_schema_types   
                    where (name='dateTime' or name='date') and kind='P'  
                    or kind='N' or kind='Z')   
               ) dttypes on scp.placed_xml_component_id=dttypes.xml_component_id  
          ) dtplaced on xsc.xml_component_id=dtplaced.xml_component_id);   
DECLARE @SchemaName nvarchar(max);   
DECLARE @TableName nvarchar(max);   
DECLARE @ColumnName nvarchar(max);   
DECLARE @strSQL nvarchar(MAX);   
OPEN C;   
FETCH NEXT FROM C INTO @SchemaName, @TableName, @ColumnName;   
WHILE (@@FETCH_STATUS = 0)   
BEGIN  
      SET @strSQL = 'INSERT INTO #_dt_collector SELECT x FROM ( ';   
      SET @strSQL = @strSQL +    
                    'SELECT ''' + @SchemaName + '.' + @TableName + '.' + @ColumnName   
                  + ''' as "@Column", ';   
      SET @strSQL = @strSQL +    
      'sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:dateTime?)])'', ''bigint'')) as "@dT_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:dateTime?)][substring(string(.),1,1) ="-"])'', ''bigint'')) as "@neg_dT_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:date?)])'', ''bigint'')) as "@date_elements"  
     , sum(' + @ColumnName + '.value(''count(//*[. instance of element(*,xs:date?)][substring(string(.),1,1) ="-"])'', ''bigint'')) as "@neg_date_elements"   
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)  
                      where $v instance of xs:dateTime?   
                      return 1)'', ''bigint'')) as "@dT_attributes"   
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:dateTime?   
                      and substring(string($v),1,1)= "-"  
                      return 1)'', ''bigint'')) as "@neg_dt_attributes"  
     , sum(' + @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:date?   
                      return 1)'', ''bigint'')) as "@date_attributes"   
     , sum('+ @ColumnName + '.value(''count(for $d in //@*, $v in data($d)   
                      where $v instance of xs:date?   
                      and substring(string($v),1,1)= "-"  
                      return 1)'', ''bigint'')) as "@neg_date_attributes"'  
      + ' FROM ' + @SchemaName + '.' + @TableName  
      + ' FOR XML PATH(''data''), type) T(x)';   
      --SELECT @strSQL;   
      EXEC sp_executesql @strSQL;   
      FETCH NEXT FROM C INTO @SchemaName, @TableName, @ColumnName;   
END;   
CLOSE C;   
DEALLOCATE C;   
SELECT x as "*" FROM #_dt_collector for xml path(''), root('data');   
drop table #_dt_collector;   
END;   
go  
-- Get the dependent columns per affected XML Schema Collection and the  
-- number of affected values  
EXECUTE DateTimeInvestigation 1;   
```  
  
 Se vengono individuati valori di anni negativi, sono disponibili più soluzioni:  
  
-   Eliminare le righe.  
  
-   Aggiornare tali valori.  
  
-   Cancellare l'intera colonna XML.  
  
-   Ritipizzare la colonna XML con una raccolta di schemi che non utilizza xs:date o xs:dateTime (utilizzare ad esempio xs:string)  
  
 Dopo avere risolto i problemi relativi ad anni negativi, è possibile eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Per utilizzare indici XML in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], dopo l'aggiornamento è necessario ricompilare gli indici XML o ritipizzare le colonne XML per tutte le colonne che utilizzano xs:date, xs:time o xs:dateTime.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
