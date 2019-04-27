---
title: Contrassegnare gli oggetti Business come sicuri per lo Scripting | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 729daea7fe719f33ec8931424143c3fedc5ac86f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62675917"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>Contrassegnare gli oggetti business come sicuri per lo scripting
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Per garantire un ambiente Internet protetto, è necessario contrassegnare tutti gli oggetti business istanziati con il [Servizi Desktop remoto. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) dell'oggetto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) metodo come "sicuri per lo script". È necessario verificare che siano contrassegnati come tale nell'area di licenza del Registro di sistema prima di poter essere utilizzati in DCOM.  
  
> [!NOTE]
>  Gli oggetti business contrassegnati come "sicuri per lo script" o sicure per l'inizializzazione possono essere creata un'istanza e inizializzati da chiunque in rete. Contrassegno di un oggetto business "sicuri" non lo rende sicuro. È estremamente importante per assicurarsi che gli oggetti business sono codificati con la massima protezione per garantire che tali oggetti non dispongono di un punto di accesso non protetto per i dati sensibili.  
  
 Per contrassegnare manualmente gli oggetti business come sicuri per lo script, creare un file di testo con estensione reg contenente il testo seguente. In questo esempio \< *MyActiveXGUID*> è il numero GUID esadecimale dell'oggetto business. I seguenti due numeri abilitare la funzionalità safe per lo scripting:  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 Salvare il file e unirlo del Registro di sistema usando l'Editor del Registro di sistema o fare doppio clic sul file con estensione reg in Esplora Windows.  
  
 Gli oggetti business creati in Microsoft Visual Basic possono essere contrassegnati automaticamente come "sicuri" con il pacchetto e distribuzione guidata. Quando viene richiesto di specificare le impostazioni di sicurezza, selezionare **sicure per l'inizializzazione** e **sicuri per lo script**.  
  
 Nel passaggio precedente, l'installazione guidata applicazione crea un file. htm e un file con estensione cab. È quindi possibile copiare questi due file nel computer di destinazione e fare doppio clic sul file htm per caricare la pagina e registrare correttamente il server.  
  
 L'oggetto business sarà installato nella directory Windows\System32\Occache per impostazione predefinita, spostarlo nella directory Windows\System32 e modificare il **HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32** chiave del Registro di sistema in base al percorso corretto.


