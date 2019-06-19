---
title: Uso di ADO con linguaggi di Scripting | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d41d5a0239f11882c135c27fd4af8e817e83b799
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702769"
---
# <a name="using-ado-with-scripting-languages"></a>Uso di ADO con i linguaggi di scripting
All'interno di un ambiente di scripting, ADO consente di esporre i dati tramite gli script lato server. In questo scenario, ADO, il provider OLE DB sottostante che viene utilizzato e vengono installati altri componenti necessari per fare riferimento a un archivio dati specificato in un server che esegue Internet Information Services (IIS). Usando le pagine ASP (Active Server), ADO è un componente di cui viene fatto riferimento in uno script che può generare codice HTML, ad esempio. Il contenuto HTML può essere passato tramite HTTP in un Web browser client. Tramite la creazione di script, la pagina Web può inviare azioni torna allo script sul lato server, in modo da aggiornare, attraversare o visualizzare i dati specifici.  
  
 Prima di usare un oggetto ActiveX in una pagina Web, è importante sapere se l'oggetto è sicuro per lo scripting. Quando un oggetto è considerato sicuro per lo scripting, significa che il controllo non può intraprendere alcuna azione dannoso nel computer dell'utente e pertanto può essere eseguito senza richiedere l'approvazione dell'utente. Nella tabella seguente sono elencati gli oggetti ADO e indica se sono sicuri per lo script.  
  
|Object|È sicuro per lo Scripting?|  
|------------|-------------------------|  
|Connessione di ADO|Yes|  
|Comando ADO|No|  
|Parametro ADO|No|  
|ADO Recordset|Yes|  
|ADO Record|Yes|  
|Stream ADO|Yes|  
|Errore ADO|No|  
|Catalogo ADOX|No|  
|ADOX CellSet|no|  
|Servizi Desktop remoto DataControl|Yes|  
|DataSpace Servizi Desktop remoto|Yes|  
|Data factory di servizi desktop remoto|No|  
  
 Nella tabella seguente sono elencati i provider inclusi con Windows DAC o MDAC e indica se sono sicuri per lo script.  
  
|Provider|È sicuro per lo Scripting?|  
|--------------|-------------------------|  
|Con forme|Yes|  
|Salvare in modo permanente|Yes|  
|Remote|Yes|  
|Provider OLE DB per SQL Server (SQLOLEDB)|No|  
|Provider OLE DB per ODBC (MSDASQL)|No|  
  
## <a name="odbc-data-sources"></a>Origini dei dati ODBC  
 Una differenza rilevante tra il codice ADO di scripting e non di script è l'origine dati ODBC, se utilizzato. Per le applicazioni non di script, è possibile creare un DSN utente in Amministrazione origine dati ODBC. Per gli script in esecuzione in IIS, è necessario creare un DSN di sistema. in caso contrario, gli script non riconoscerà l'origine dati creata. Questo vale per qualsiasi applicazione di scripting di ADO con il Provider Microsoft OLE DB per ODBC tramite Microsoft IIS.  
  
## <a name="referencing-the-ado-library"></a>Riferimento alla libreria ADO  
 Non applicabile con linguaggi di scripting.  
  
## <a name="handling-events"></a>Gestione degli eventi  
 Non applicabile con linguaggi di scripting.  
  
 Gli argomenti seguenti contengono informazioni più specifiche sull'uso di ADO con linguaggi di scripting:  
  
-   [Programmazione ADO VBScript](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [Programmazione ADO JScript](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Uso di ADO con Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Uso di ADO con Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
