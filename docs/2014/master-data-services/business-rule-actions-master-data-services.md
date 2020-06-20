---
title: Azioni della regola di business (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cdc4daca-3dff-46d8-b7f0-57f7826dd61a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 188551ec988bfd71a54f0a56b6180cb92defc2bb
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972142"
---
# <a name="business-rule-actions-master-data-services"></a>Azioni Regola business (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], le azioni della regola business sono la conseguenza delle valutazioni sulle condizioni della regola business. Se una condizione è vera, l'azione viene avviata.  
  
> [!NOTE]  
>  Per le azioni di tipo Valore predefinito e Modifica valore, se il valore generato supera la lunghezza massima dell'attributo, viene troncato il valore generato.  
  
## <a name="default-value-actions"></a>Azioni Valori predefinito  
 Le azioni di tipo**Valore predefinito** determinano l'impostazione del valore predefinito di un attributo specificato. Gli utenti che dispongono delle autorizzazioni necessarie possono modificare questi valori predefiniti.  
  
|Nome del valore|Description|  
|----------------|-----------------|  
|**assume il valore**|L'attributo selezionato **assume il valore** di un attributo specifico o di un valore di attributo specifico oppure è vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici, di data e di collegamento.|  
|**assume un valore generato**|L'attributo selezionato **assume un valore generato** determinato dall'immissione di un valore iniziale e incrementale.<br /><br /> Questa azione è valida per valori di testo e numerici.|  
|**assume un valore concatenato**|L'attributo selezionato **assume un valore concatenato** determinato mediante la specifica di più attributi.<br /><br /> Questa azione è valida per valori di testo e di collegamento.|  
  
## <a name="change-value-actions"></a>Azioni Modifica valore  
 Le azioni di tipo**Modifica valore** determinano l'aggiornamento del valore di un attributo o di un valore di attributo specificato. Gli utenti possono modificare questi valori solo se il nuovo valore rende vera l'azione.  
  
|Nome del valore|Description|  
|----------------|-----------------|  
|**Uguale a**|L'attributo selezionato viene modificato in un valore di attributo definito, in un altro attributo o in un valore vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici, di data e di collegamento.|  
|**uguale a un valore concatenato**|L'attributo selezionato viene modificato in un valore concatenato determinato mediante la specifica di più attributi.<br /><br /> Questa azione è valida per valori di testo e di collegamento.|  
  
## <a name="validation-actions"></a>Azioni Convalida  
 Le azioni di tipo**Convalida** , quando non restituiscono true, determinano l'invio di un messaggio di posta elettronica a un utente o gruppo specificato. Per eseguire il commit di una versione, tutte le azioni di convalida devono restituire true.  
  
 Le uniche eccezioni sono costituite dalle azioni **è obbligatorio** e **non è valido** . Queste azioni devono essere combinate con un'azione di modifica del valore, in modo che i dati possano essere convalidati e venga eseguito il commit della versione.  
  
|Nome della convalida|Description|  
|---------------------|-----------------|  
|**è obbligatorio**|L'attributo selezionato **è obbligatorio**, ovvero non può essere null o vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici, di data e di collegamento.|  
|**non è valido**|L'attributo selezionato **non è valido**.<br /><br /> Questa azione è valida per valori di testo, numerici, di data e di collegamento.|  
|**deve contenere il modello**|L'attributo selezionato **deve contenere il modello** specificato. Utilizzare le espressioni regolari di .NET Framework per specificare il modello.<br /><br /> Per ulteriori informazioni su espressioni regolari, vedere [Elementi del linguaggio di espressioni regolari](https://go.microsoft.com/fwlink/?LinkId=164401) in MSDN Library.<br /><br /> Questa azione è valida per valori di testo e di collegamento.|  
|**deve essere univoco**|L'attributo selezionato **deve essere univoco** in modo indipendente o in combinazione con gli attributi definiti.<br /><br /> **Procedura consigliata:** combinare questa azione con una condizione obbligatoria per garantire la validità dei campi di indice nei sistemi di sottoscrizione.<br /><br /> Questa azione è valida per valori di testo, numerici, di data e di collegamento.|  
|**deve avere uno dei seguenti valori**|L'attributo selezionato **deve avere uno dei seguenti valori** specificati in un elenco.<br /><br /> Questa azione è valida per valori di testo.|  
|**deve essere maggiore di**|L'attributo selezionato **deve essere maggiore di** un attributo specifico o di un valore di attributo specifico oppure deve essere vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici e di data.|  
|**deve essere uguale a**|L'attributo selezionato **deve essere uguale a** un valore di attributo definito o a un altro attributo oppure deve essere vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici, di data e di collegamento.|  
|**deve essere maggiore o uguale a**|L'attributo selezionato **deve essere maggiore o uguale a** un attributo specifico o a un valore di attributo specifico oppure deve essere vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici e di data.|  
|**deve essere minore di**|L'attributo selezionato **deve essere minore di** un attributo specifico o di un valore di attributo specifico oppure deve essere vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici e di data.|  
|**deve essere minore o uguale a**|L'attributo selezionato **deve essere minore o uguale a** un attributo specifico o a un valore di attributo specifico oppure deve essere vuoto.<br /><br /> Questa azione è valida per valori di testo, numerici e di data.|  
|**deve essere compreso tra**|L'attributo selezionato **deve essere compreso tra** due attributi o valori di attributo specifici.<br /><br /> Questa azione è valida per valori di testo, numerici e di data.|  
|**deve avere una lunghezza uguale o maggiore di**|L'attributo selezionato **deve avere una lunghezza uguale o maggiore di** quella del valore specificato.<br /><br /> Questa azione è valida per valori di testo e di collegamento.|  
|**deve avere una lunghezza minore o uguale a**|L'attributo selezionato **deve avere una lunghezza minore o uguale a** quella del valore specificato.<br /><br /> Questa azione è valida per valori di testo e di collegamento.|  
  
## <a name="external-action"></a>Azione esterna  
 Le**azioni esterne** interagiscono con le applicazioni al di fuori di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
|Nome dell'azione|Description|  
|-----------------|-----------------|  
|**avvia il flusso di lavoro**|Avvia un flusso di lavoro esterno. I dati che hanno causato questa azione vengono passati al flusso di lavoro. Per ulteriori informazioni, vedere [Integrazione del flusso di lavoro SharePoint con Master Data Services](https://msdn.microsoft.com/library/gg690195.aspx).<br /><br /> Questa azione è valida per valori di testo, numerici, di data e di collegamento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Condizioni della regola business &#40;Master Data Services&#41;](business-rule-conditions-master-data-services.md)   
 [Regole business &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Creare e pubblicare una regola business &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
