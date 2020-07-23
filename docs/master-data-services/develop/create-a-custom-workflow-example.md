---
title: Esempio di flusso di lavoro personalizzato
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 404fab4ed966fd8b29bc4160e7a7d721dd6397e7
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923085"
---
# <a name="create-a-custom-workflow---example"></a>Creare un flusso di lavoro personalizzato - Esempio

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Quando in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] si crea una libreria di classi del flusso di lavoro personalizzato, viene creata una classe che implementa l'interfaccia Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender. Questa interfaccia include un metodo, [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) , che viene chiamato da SQL Server servizio di integrazione del flusso di lavoro MDS all'avvio di un flusso di lavoro. Il metodo [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) contiene due parametri: *WorkflowType* contiene il testo immesso nella casella di testo **tipo di flusso di lavoro** in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e *dataElement* contiene i metadati e i dati dell'elemento che ha attivato la regola business del flusso di lavoro.  
  
## <a name="custom-workflow-example"></a>Esempio di flusso di lavoro personalizzato  
 Nell'esempio di codice seguente viene illustrato come implementare il metodo [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) per estrarre gli attributi Name, code e LastChgUserName dai dati XML per l'elemento che ha attivato la regola business del flusso di lavoro e come chiamare un stored procedure per inserirli in un altro database. Per un esempio del codice XML dei dati dell'elemento e per una spiegazione dei tag in esso contenuti, vedere [Descrizione XML del flusso di lavoro personalizzato &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("./MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("./MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("./MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un flusso di lavoro personalizzato &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
