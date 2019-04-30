---
title: Proprietà ConnectionString (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01a930bc571e84c6ecfd38ce8415493c90ebd377
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140359"
---
# <a name="connectionstring-property-ado"></a>Proprietà ConnectionString (ADO)
Indica le informazioni utilizzate per stabilire una connessione a un'origine dati.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore.  
  
## <a name="remarks"></a>Note  
 Usare la **ConnectionString** proprietà per specificare un'origine dati passando una stringa di connessione dettagliati contenente una serie di *argomento* *= valore* istruzioni separate da punto e virgola.  
  
 ADO supporta cinque argomenti per il **ConnectionString** proprietà; qualsiasi altro passaggio di argomenti direttamente al provider senza alcuna elaborazione da parte di ADO. ADO supporta gli argomenti è i seguenti.  
  
|Argomento|Descrizione|  
|--------------|-----------------|  
|*Provider=*|Specifica il nome di un provider da utilizzare per la connessione.|  
|*Nome file =*|Specifica il nome di un file specifico del provider (ad esempio, un oggetto origine dati persistenti) che contiene informazioni di connessione predefinite.|  
|*Provider remoto =*|Specifica il nome di un provider da utilizzare quando si apre una connessione client-side. (Solo servizio dati remoto).|  
|*Server remoto =*|Specifica il nome del percorso del server da usare quando si apre una connessione client-side. (Solo servizio dati remoto).|  
|*URL=*|Specifica la stringa di connessione come un URL assoluto che identifica una risorsa, ad esempio un file o directory.|  
  
 Dopo aver impostato la **ConnectionString** proprietà e aprire il [connessione](../../../ado/reference/ado-api/connection-object-ado.md) dell'oggetto, il provider può modificare il contenuto della proprietà, ad esempio, eseguendo il mapping di nomi degli argomenti definiti da ADO per loro equivalenti per il provider specifico.  
  
 Il **ConnectionString** proprietà eredita automaticamente il valore usato per il *ConnectionString* argomento del [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo, pertanto è possibile eseguire l'override corrente **ConnectionString** proprietà durante il **Open** chiamata al metodo.  
  
 Poiché il *nome File* argomento causa ADO caricare il provider associato, non è possibile passare sia la *Provider* e *nome File* argomenti.  
  
 Il **ConnectionString** è di lettura/scrittura quando la connessione è chiusa e di sola lettura quando è aperto.  
  
 I duplicati di un argomento in di **ConnectionString** proprietà vengono ignorate. Viene usato l'ultima istanza di un argomento.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Connection** oggetto, il **ConnectionString** può includere solo proprietà il *Provider remoto* e *Server remoto* parametri.  
  
 La tabella seguente elenca il provider ADO predefinito per ogni sistema operativo Windows:  
  
|Provider predefinito di ADO|Sistema operativo Windows|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (Per migliorare la leggibilità del codice sorgente, specificare in modo esplicito il nome del provider nella stringa di connessione.)|Windows 2000 (32-bit)<br /><br /> Windows XP (32-bit)<br /><br /> Windows 2003 Server (32 bit)<br /><br /> Windows Vista (32 bit)<br /><br /> Windows Vista Service Pack 1 o versioni successive (32 bit e 64 bit)<br /><br /> Versioni di Windows dopo Windows Vista (32 bit e 64 bit)|  
|Nessuna impostazione predefinita.<br /><br /> Quando un'applicazione ADO esegue nei seguenti sistemi operativi e non specifica il provider in modo esplicito, ADO restituisce l'errore seguente: "ADODB. Connessione: provider non è specificato e non vi è alcun provider predefinito designato "|Windows 2000 (64-bit)<br /><br /> Windows XP (64-bit)<br /><br /> Windows 2003 Server (64 bit)<br /><br /> Windows Vista (64-bit)|  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ConnectionString, ConnectionTimeout ed esempio di proprietà State (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Esempio ConnectionString, ConnectionTimeout e proprietà State (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Appendice a: Providers](../../../ado/guide/appendixes/appendix-a-providers.md)
