---
description: Nozioni fondamentali su ADOX
title: Nozioni fondamentali su ADOX | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADOX, fundamentals
ms.assetid: 954476fc-5f72-4ada-ace5-d9acb27d18f8
author: rothja
ms.author: jroth
ms.openlocfilehash: d24e7a61642ed9945dfc69a06c584b2423775659
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978702"
---
# <a name="adox-fundamentals"></a>Nozioni fondamentali su ADOX
Microsoft® ActiveX® Data Objects Extensions for Data Definition Language and Security (ADOX) è un'estensione degli oggetti ADO e del modello di programmazione. ADOX include oggetti per la creazione e la modifica dello schema, nonché per la sicurezza. Poiché si tratta di un approccio basato su oggetti alla manipolazione dello schema, è possibile scrivere codice che funzionerà su varie origini dati indipendentemente dalle differenze nelle relative sintassi native.  
  
 ADOX è una libreria complementare agli oggetti ADO di base. Espone oggetti aggiuntivi per la creazione, la modifica e l'eliminazione di oggetti dello schema, ad esempio tabelle e procedure. Include inoltre oggetti di sicurezza per gestire utenti e gruppi e per concedere e revocare le autorizzazioni per gli oggetti.  
  
 Per usare ADOX con lo strumento di sviluppo, è necessario definire un riferimento alla libreria dei tipi ADOX. La descrizione della libreria ADOX è "Microsoft ADO Ext. per DDL e sicurezza". Il nome del file della libreria ADOX è Msadox.dll e l'ID del programma (ProgID) è "ADOX". Per ulteriori informazioni sulla definizione dei riferimenti alle librerie, vedere la documentazione dello strumento di sviluppo.  
  
 Il provider Microsoft OLE DB per Microsoft Jet motore di database supporta completamente ADOX. Alcune funzionalità di ADOX potrebbero non essere supportate, a seconda del provider di dati.  
  
 In questo documento si presuppone una conoscenza approfondita di Microsoft® Visual Basic® linguaggio di programmazione e una conoscenza generale di ADO. Per ulteriori informazioni su ADO, vedere la [Guida per programmatori ADO](../ado-programmer-s-guide.md). Per ulteriori informazioni generali su ADOX, vedere gli argomenti seguenti:  
  
-   [Modello a oggetti ADOX](../../reference/adox-api/adox-object-model.md)  
  
-   [Oggetti ADOX](../../reference/adox-api/adox-objects.md)  
  
-   [Raccolte ADOX](../../reference/adox-api/adox-collections.md)  
  
-   [Proprietà ADOX](../../reference/adox-api/adox-properties.md)  
  
-   [Metodi ADOX](../../reference/adox-api/adox-methods.md)  
  
-   [Esempi di ADOX](../../reference/adox-api/adox-code-examples.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sull'API ADOX](../../reference/adox-api/adox-object-model.md?view=sql-server-ver15)   
 [Esempi di codice ADOX](../../reference/adox-api/adox-code-examples.md)   
 [Raccolte ADOX](../../reference/adox-api/adox-collections.md)   
 [Costanti enumerate ADOX](../../reference/adox-api/adox-enumerated-constants.md)   
 [Metodi ADOX](../../reference/adox-api/adox-methods.md)   
 [Modello a oggetti ADOX](../../reference/adox-api/adox-object-model.md)   
 [Oggetti ADOX](../../reference/adox-api/adox-objects.md)   
 [Proprietà di ADOX](../../reference/adox-api/adox-properties.md)   
 [ADO (multidimensionale) (ADO MD)](../multidimensional/ado-multidimensional-ado-md.md)   
 [Manuale del programmatore ADO](../ado-programmer-s-guide.md)