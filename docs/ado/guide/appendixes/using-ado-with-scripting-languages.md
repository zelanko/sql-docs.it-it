---
title: Utilizzo di ADO con i linguaggi di scripting | Microsoft Docs
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
ms.openlocfilehash: 6b322dacbf85ec24b58e315ecbbf9d547d1481f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926486"
---
# <a name="using-ado-with-scripting-languages"></a>Uso di ADO con i linguaggi di scripting
All'interno di un ambiente di scripting, ADO consente di esporre i dati tramite scripting lato server. In questo scenario, ADO, il provider OLE DB sottostante utilizzato e tutti gli altri componenti necessari per fare riferimento a un determinato archivio dati vengono installati in un server che esegue Internet Information Services (IIS). Utilizzando Active Server Pages (ASP), ADO è un componente a cui viene fatto riferimento in uno script in grado di generare codice HTML, ad esempio. Questo contenuto HTML può essere passato tramite HTTP a un Web browser client. Utilizzando lo scripting, la pagina Web può inviare azioni allo script sul lato server, consentendo di aggiornare, attraversare o visualizzare dati specifici.  
  
 Prima di utilizzare un oggetto ActiveX in una pagina Web, è importante sapere se l'oggetto è sicuro per lo scripting. Quando un oggetto viene considerato sicuro per lo scripting, significa che il controllo non può eseguire alcuna azione dannosa sul computer dell'utente e pertanto può essere eseguito senza richiedere l'approvazione dell'utente. Nella tabella seguente sono elencati gli oggetti ADO e viene indicato se sono sicuri per lo scripting.  
  
|Oggetto|Sicuro per gli script?|  
|------------|-------------------------|  
|Connessione ADO|Sì|  
|Comando ADO|No|  
|ADO-parametro|No|  
|Recordset ADO|Sì|  
|Record ADO|Sì|  
|Flusso ADO|Sì|  
|Errore ADO|No|  
|Catalogo ADOX|No|  
|ADOX di celle|No|  
|Controllo Servizi Desktop remoto|Sì|  
|Spazio di servizi RDS|Sì|  
|Datafactory RDS|No|  
  
 Nella tabella seguente sono elencati i provider inclusi in Windows DAC/MDAC e viene indicato se sono sicuri per lo scripting.  
  
|Provider|Sicuro per gli script?|  
|--------------|-------------------------|  
|Con forme|Sì|  
|Persist|Sì|  
|Remote|Sì|  
|Provider di OLE DB per SQL Server (SQLOLEDB)|No|  
|Provider di OLE DB per ODBC (MSDASQL)|No|  
  
## <a name="odbc-data-sources"></a>Origini dei dati ODBC  
 Una differenza rilevante tra lo scripting e il codice ADO non di scripting è l'origine dati ODBC, se utilizzata. Per le applicazioni non di scripting, è possibile creare un DSN utente in Amministrazione origine dati ODBC. Per gli script in esecuzione in IIS, è necessario creare un DSN di sistema. in caso contrario, gli script non rileveranno l'origine dati creata. Si applica a qualsiasi applicazione di scripting ADO che utilizza il provider Microsoft OLE DB per ODBC tramite Microsoft IIS.  
  
## <a name="referencing-the-ado-library"></a>Riferimento alla libreria ADO  
 Non applicabile ai linguaggi di scripting.  
  
## <a name="handling-events"></a>Gestione degli eventi  
 Non applicabile ai linguaggi di scripting.  
  
 Negli argomenti seguenti sono contenute informazioni più specifiche sull'utilizzo di ADO con i linguaggi di scripting:  
  
-   [Programmazione ADO VBScript](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [Programmazione ADO JScript](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Utilizzo di ADO con Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Uso di ADO con Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
