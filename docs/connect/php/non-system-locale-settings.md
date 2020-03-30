---
title: Impostazioni locali non di sistema | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- locale, linux, macOS, system
author: yitam
ms.author: v-yitam
manager: v-mabarw
ms.openlocfilehash: bd60bff3ab9ee19b1a1d2435e69651ea054689e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "76913324"
---
# <a name="non-system-locale-settings"></a>Impostazioni locali non di sistema
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Questa sezione si applica solo agli utenti Linux e macOS, in particolare quelli che gestiscono più impostazioni locali nelle applicazioni PHP.

Per impostazione predefinita, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] accetta la variabile di ambiente `LC_ALL` definita nel sistema ed esegue l'override di tutte le altre categorie di `LC_xxx` (ad eccezione `$LANG` o `$LANGUAGE` in alcune circostanze), che influiscono su separatore delle migliaia, carattere del separatore decimale, set di caratteri, mese, nomi dei giorni, messaggi dell'applicazione (ad esempio i messaggi di errore), simbolo di valuta e altro ancora.

A partire dalla versione 5.8.0, gli utenti possono configurare le impostazioni di localizzazione usando il file php.ini, come illustrato negli esempi seguenti.

## <a name="set-locale-info-using-the-sqlsrv-driver"></a>Impostare le informazioni sulle impostazioni locali usando il driver SQLSRV  
Aggiungere quanto segue alla fine del file php.ini:
  
```  
[sqlsrv]  
sqlsrv.SetLocaleInfo = <option>
```  
  
## <a name="set-locale-info-using-the-pdo_sqlsrv-driver"></a>Impostare le informazioni sulle impostazioni locali usando il driver PDO_SQLSRV  
Aggiungere quanto segue alla fine del file php.ini:
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.set_locale_info = <option>
```  
  
L'**opzione** può essere uno dei valori seguenti:  
  
|Opzione|Descrizione del comportamento|
|---------|---------------|
|0|Il driver ignora le impostazioni locali del sistema.|
|1|Il driver legge la variabile LC_CTYPE.|
|2|Il driver legge la variabile LC_ALL (impostazione predefinita).|
  

La categoria `LC_CTYPE` determina le regole di gestione dei caratteri, che regolano l'interpretazione di sequenze di byte di caratteri dei dati di testo, la classificazione dei caratteri e il comportamento delle classi di caratteri. Controlla il riconoscimento dei caratteri maiuscoli e minuscoli, alfabetici e non alfabetici e così via.

### <a name="explanation"></a>Spiegazione

1. Opzione 0: usarla quando non si vogliono modificare le impostazioni locali dell'applicazione.

1. Opzione 1: usarla per impostare solo il valore di sistema di `LC_CTYPE` senza influire sulle altre categorie di `LC_xxx`.

1. Opzione 2: usare `LC_ALL` per eseguire l'override di tutte le categorie di `LC_xxx`, che interessano l'applicazione PHP e le relative estensioni.

Se le impostazioni locali per uno script PHP non sono uguali a quelle del sistema, potrebbe essere necessario specificare le impostazioni locali negli script PHP chiamando la funzione PHP predefinita [setlocale](https://www.php.net/manual/en/function.setlocale.php). 

Se, ad esempio, il valore predefinito di sistema è `en_US.UTF-8` ma lo script PHP usa `de_DE.UTF-8`, chiamare la funzione PHP `setlocale()` in modo appropriato.

Per l'opzione 2, indicare negli script PHP le impostazioni locali da usare solo se sono diverse dalla variabile `LC_ALL`.

> [!NOTE]
> Se non è stato definito alcun elemento in php.ini, l'impostazione predefinita attualmente è eseguire l'override di tutte le altre impostazioni locali in base a `LC_ALL`, che verrà **deprecato**. Nel prossimo futuro, per impostazione predefinita verranno ignorate le impostazioni locali del sistema. Pertanto, gli utenti dovranno modificare il file php.ini di conseguenza se vogliono mantenere il comportamento corrente.

Se i driver sqlsrv e pdo_sqlsrv sono entrambi abilitati, non è consigliabile impostare opzioni diverse per i due driver.