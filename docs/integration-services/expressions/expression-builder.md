---
title: Generatore di espressioni | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionbuilder.f1
helpviewer_keywords:
- Expression Builder dialog box
ms.assetid: 4717ce33-bd4e-44bc-81e0-002de075b4d1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 04457acc8bd47f3802ba7ad68797d1745117871d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725416"
---
# <a name="expression-builder"></a>Generatore di espressioni

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Usare la finestra di dialogo **Generatore di espressioni** per creare e modificare un'espressione di proprietà o scrivere l'espressione che imposta il valore di una variabile tramite un'interfaccia utente grafica in cui sono elencate variabili ed è specificato un riferimento predefinito alle funzioni, i cast di tipo e gli operatori inclusi nel linguaggio delle espressioni di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Un'espressione di proprietà è un'espressione assegnata a una proprietà. Quando l'espressione viene valutata, la proprietà viene aggiornata in modo dinamico per utilizzare il risultato della valutazione dell'espressione. In modo analogo, un'espressione utilizzata in una variabile consente l'aggiornamento del valore della variabile con il risultato della valutazione dell'espressione.  
  
 Esistono diversi modi per utilizzare le espressioni.  
  
-   **Attività** Aggiornare la riga A usata da un'attività Invia messaggi mediante l'inserimento di un indirizzo di posta elettronica memorizzato in una variabile o aggiornare la riga Oggetto mediante la concatenazione di una stringa come "Vendite per: " e la data corrente restituita dalla funzione GETDATE.  
  
-   **Variabili** Impostare il valore di una variabile sul mese corrente utilizzando un'espressione quale `DATEPART("mm",GETDATE())`oppure impostare il valore di una stringa mediante la concatenazione del valore letterale della stringa e della data corrente utilizzando l'espressione `"Today's date is " + (DT_WSTR,30)(GETDATE())`.  
  
-   **Gestioni connessioni** Impostare la tabella codici di una gestione connessioni file flat utilizzando una variabile che contiene un identificatore di tabella codici diverso oppure specificare il numero di righe da ignorare nel file di dati immettendo nell'espressione un valore integer positivo, ad esempio 3.  
  
 Per sapere di più sulle espressioni di proprietà e sulla scrittura di espressioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md) e [Espressioni di Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md).  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Variabili**|Espandere la cartella **Variabili** e trascinare le variabili nella casella **Espressione** .|  
|**Funzioni matematiche**<br /><br /> **Funzioni per i valori stringa**<br /><br /> **Funzioni di data/ora**<br /><br /> **Funzioni NULL**<br /><br /> **Cast di tipo**<br /><br /> **Operatori**|Espandere le cartelle e trascinare le funzioni, i cast di tipo e gli operatori nella casella **Espressione** .|  
|**Espressione**|Consente di modificare o digitare un'espressione.|  
|**Valore valutato**|Indica il valore restituito dall'espressione.|  
|**Valuta espressione**|Fare clic su **Valuta espressione** per visualizzare i valori restituiti dell'espressione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)   
 [Editor espressioni di proprietà](../../integration-services/expressions/property-expressions-editor.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Variabili di sistema](../../integration-services/system-variables.md)  
  
  
