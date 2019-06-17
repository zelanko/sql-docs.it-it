---
title: Rappresentazione di una connessione (tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 4b410b16-d36e-4185-bb20-922e66e5e2b7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ffd99068db329ea8e9066c6bd9508dc13f239690
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62757773"
---
# <a name="connection-representation-tabular"></a>Rappresentazione di una connessione (tabulare)
  L'oggetto connessione definisce l'origine dei dati che popolano il modello tabulare.  
  
## <a name="connection-representation"></a>Rappresentazione di una connessione  
 La specifica dell'oggetto connessione segue le regole dei provider OLE DB.  
  
### <a name="connection-in-amo"></a>Connessione in AMO  
 Quando si utilizza AMO (Analysis Management Objects) per gestire un database modello tabulare, l'oggetto <xref:Microsoft.AnalysisServices.DataSource> ha una corrispondenza uno-a-uno in AMO (Analysis Management Objects) con l'oggetto logico di connessione.  
  
 Nel frammento di codice seguente viene mostrato come creare un'origine dati AMO o un oggetto Connection in un modello tabulare.  
  
```  
  
//Create an OLEDB connection string  
StringBuilder SqlCnxStr = new StringBuilder();  
SqlCnxStr.Append(String.Format("Data Source={0};" ,SQLServer.Text));  
SqlCnxStr.Append(String.Format("Initial Catalog={0};", SQLDatabase.Text));  
SqlCnxStr.Append(String.Format("Persist Security Info={0};", false));  
SqlCnxStr.Append(String.Format("Integrated Security={0};", "SSPI"));  
SqlCnxStr.Append(String.Format("Provider={0}", "SQLNCLI11"));  
String DatasourceCnxString = SqlCnxStr.ToString();  
  
//Verify connection string and connectivity  
System.Data.OleDb.OleDbConnection OleDbCnx = new System.Data.OleDb.OleDbConnection(DatasourceCnxString);  
try  
{  
    OleDbCnx.Open();  
}  
catch ()  
{  
    throw;  
}  
String newDataSourceName = (string.IsNullOrEmpty(DataSourceName.Text) || string.IsNullOrWhiteSpace(DataSourceName.Text)) ? SQLDatabase.Text : DataSourceName.Text;  
AMO.DataSource newDatasource = newDatabase.DataSources.Add(newDataSourceName, newDataSourceName);  
newDatasource.ConnectionString = DatasourceCnxString.Text;  
if (impersonateServiceAccount.Checked)  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateServiceAccount);  
else  
{  
    if (String.IsNullOrEmpty(impersonateAccountUserName.Text))  
    {  
        MessageBox.Show(String.Format("Account User Name cannot be blank when using 'ImpersonateAccount' mode"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        return;  
    }  
    newDatasource.ImpersonationInfo = new AMO.ImpersonationInfo(AMO.ImpersonationMode.ImpersonateAccount, impersonateAccountUserName.Text, impersonateAccountPassword.Text);  
}  
newDatasource.Update();  
  
```  
  
## <a name="tabular-amo-2012-sample"></a>Esempio Tabular AMO 2012  
 Per consentire una migliore comprensione sull'utilizzo di AMO per creare e modificare le rappresentazioni di connessioni, vedere il codice sorgente nell'esempio di Tabular AMO 2012; in particolare controllare nel seguente file di origine: Database.cs. L'esempio è disponibile in Codeplex. Il codice di esempio viene fornito solo come supporto ai concetti logici illustrati in questo argomento e non deve essere utilizzato in un ambiente di produzione.  
  
  
