---
title: Oggetto DataControl (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl
- RDS.DataControl
helpviewer_keywords:
- DataControl object [ADO]
ms.assetid: d85ea4fc-451c-436e-97b8-58f92b149dd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a571e93a070c3ce07fbaf40a86b762c749042ec1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964394"
---
# <a name="datacontrol-object-rds"></a>Oggetto DataControl (Servizi Desktop remoto)
Associa una query di data [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) a uno o più controlli (ad esempio, una casella di testo, un controllo griglia o una casella combinata) per visualizzare i **Recordset** dati in una pagina Web.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
</OBJECT>  
```  
  
## <a name="remarks"></a>Note  
 L'ID della classe per il **Servizi Desktop remoto. DataControl** oggetto è BD96C556-65A3 - 11d 0-983A-00C04FC29E33.  
  
> [!NOTE]
>  Se si verifica un errore che un [Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) o **Servizi Desktop remoto. DataControl** object non caricare, assicurarsi di usare l'ID di classe corretto. La classe di ID per questi oggetti sono stati modificati dalla versione 1.0 e 1.1. Tenere anche presente che è necessario impostare le colonne nullable anche quando si usa la **Servizi Desktop remoto DataControl** oggetto.  
  
 Per uno scenario di base, è necessario impostare solo le **SQL**, **Connect**, e **Server** le proprietà del **Servizi Desktop remoto. DataControl** oggetto, che chiamerà automaticamente l'oggetto business predefinito, [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md).  
  
 Tutte le proprietà di **Servizi Desktop remoto. DataControl** sono facoltative in quanto gli oggetti business personalizzata possono sostituire le proprie funzionalità.  
  
> [!NOTE]
>  Se esegue una query per più risultati, solo le prime [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) viene restituito. Se sono necessari più set di risultati, assegnarlo a un proprio **DataControl**. Un esempio di una query per ottenere risultati più potrebbe essere come segue: `"Select * from Authors, Select * from Topics"`  
  
 Aggiunta di "DFMode = 20;" alla stringa di connessione quando si usa il **Servizi Desktop remoto. DataControl** oggetto può migliorare le prestazioni del server quando si esegue l'aggiornamento dati. Con questa impostazione, il **RDSServer** oggetti sul server utilizza una modalità meno risorse. Tuttavia, le funzionalità seguenti non sono disponibili in questa configurazione:  
  
-   Uso di query con parametri.  
  
-   Recupero di informazioni di parametro o della colonna prima di chiamare il **Execute** (metodo).  
  
-   L'impostazione **Transact Updates** al **True**.  
  
-   Ottenere lo stato di riga.  
  
-   Chiama il [Risincronizza](../../../ado/reference/ado-api/resync-method.md) (metodo).  
  
-   Aggiornamento (in modo esplicito o automaticamente) tramite il [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) proprietà.  
  
-   L'impostazione **comandi** oppure [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) proprietà.  
  
-   Usando **adCmdTableDirect**.  
  
 Il **Servizi Desktop remoto. DataControl** oggetto viene eseguito in modalità asincrona per impostazione predefinita. Se è necessaria l'esecuzione sincrona per l'applicazione, impostare il [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) uguale al parametro **adcExecSync** e il [FetchOptions](../../../ado/reference/rds-api/fetchoptions-property-rds.md) parametro con valore uguale a **adcFetchUpFront**, come illustrato nell'esempio seguente.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"   
    ID="DataControl"  
   <PARAM NAME="Connect" VALUE="DSN=DSNName;UID=MyUserID;PWD=MyPassword;">  
   <PARAM NAME="Server" VALUE="https://awebsrvr">  
   <PARAM NAME="SQL" VALUE="QueryText">  
   <PARAM NAME="ExecuteOptions" VALUE="1">   <PARAM NAME="FetchOptions" VALUE="1">  
</OBJECT>  
```  
  
 Usare uno **Servizi Desktop remoto. DataControl** oggetto per collegare i risultati di una singola query a uno o più controlli visivi. Ad esempio, si supponga che il codice di una query che richiede dati dei clienti, ad esempio nome, residenza, luogo di nascita, durata e stato di priorità del cliente. È possibile usare un singolo **Servizi Desktop remoto. DataControl** oggetto da visualizzare nome del cliente, età e area tre caselle di testo separato. Stato di priorità del cliente in una casella di controllo; e tutti i dati in un controllo griglia.  
  
 Utilizzare diverse **Servizi Desktop remoto. DataControl** gli oggetti a cui collegarsi i risultati delle query più controlli visivi diversi. Si supponga, ad esempio, che è possibile utilizzare una query per ottenere informazioni relative a un cliente e una seconda query per ottenere informazioni su denaro, merci che il cliente ha acquistato. Si desidera visualizzare i risultati della prima query in tre caselle di testo e una casella di controllo e i risultati della query secondo in un controllo griglia. Se si usa l'oggetto business predefinito (**RDSServer**), è necessario eseguire le operazioni seguenti:  
  
-   Aggiungere due **Servizi Desktop remoto. DataControl** oggetti alla pagina Web.  
  
-   Le query di scrittura due, uno per ogni **SQL** proprietà di due **Servizi Desktop remoto. DataControl** oggetti. Uno **Servizi Desktop remoto. DataControl** oggetto conterrà una query SQL che richiede informazioni sul cliente; la second conterrà una query che richiede un elenco di denaro, merci il cliente ha acquistato.  
  
-   Nel tag OBJECT di ogni controllo associato, specificare il valore DATAFLD per impostare i valori per i dati che si desidera visualizzare in ogni controllo visuale.  
  
 Non vi è alcuna restrizione conteggio sul numero di **Servizi Desktop remoto. DataControl** gli oggetti che è possibile incorporare con tag di oggetti in una singola pagina Web.  
  
 Quando si definisce la **Servizi Desktop remoto. DataControl** dell'oggetto in una pagina Web, usare diverso da zero **altezza** e **larghezza** valori, ad esempio 1 (per evitare l'inclusione di spazio aggiuntivo).  
  
 Componenti client di servizio dati remoto sono già inclusi come parte di Internet Explorer 4.0. Pertanto, non è necessario includere un parametro CODEBASE nel **Servizi Desktop remoto. DataControl** tag object.  
  
 Con Internet Explorer 4.0 o versioni successive, è possibile associare ai dati usando i controlli HTML e ActiveX® solo se sono contrassegnati come controlli del modello di apartment.  
  
> [!NOTE]
>  **Gli utenti di Microsoft Visual Basic** il **Servizi Desktop remoto. DataControl** è sicuro per gli script e viene usato solo nelle applicazioni basate su Web. Un'applicazione client di Visual Basic non è necessario specificare per tale.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi dell'oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di oggetto DataControl (VBScript)](../../../ado/reference/rds-api/datacontrol-object-example-vbscript.md)






















