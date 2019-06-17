---
title: "Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Ruby | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ff03ce6ec79aede2e056f0154836e77970af9c50
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800824"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Ruby
È necessario configurare l'ambiente di sviluppo con i prerequisiti per lo sviluppo di un'applicazione usando il Driver Ruby per SQL Server.    
  
Si noti che il Driver Ruby Usa il protocollo TDS, che è abilitato per impostazione predefinita in SQL Server e Database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Scarica programma di installazione di Ruby**  
Se il computer non ha Ruby installarlo. Per i nuovi utenti ruby, è consigliabile che usare i programmi di installazione di Ruby 2.2.X. Forniscono un linguaggio stabile e un elenco completo dei pacchetti (gems) che sono compatibili e aggiornate. Passare il [pagina di download Ruby](https://rubyinstaller.org/downloads/) e scaricare il programma di installazione 2.1.x appropriato. Per esempio, se si usa un computer a 64 bit, scaricare il programma di installazione di Ruby 2.1.6 la proprietà (x64).   
  
2.  **Installare Ruby**  
Dopo aver scaricato il programma di installazione, eseguire le operazioni seguenti:  
A. Fare doppio clic sul file per avviare il programma di installazione.  
B. Selezionare la lingua e accettare le condizioni.  
c.  Nella schermata delle impostazioni di installazione, selezionare le caselle di controllo accanto a entrambi i file eseguibili Ruby aggiungere ai file RB e .rbw percorso ed eseguire l'associazione con questa installazione di Ruby.  
  
3.  **Scaricare DevKit Ruby**  
Scaricare DevKit dalla pagina RubyInstaller  
  
4.  **Installare Ruby DevKit**  
Una volta completato il download, eseguire le operazioni seguenti:  
A. Fare doppio clic sul file. Verrà richiesto la posizione in cui estrarre i file.  
B. Fare clic sul pulsante "..." e selezionare "C:\DevKit". Si sarà probabilmente necessario creare questa cartella prima di tutto, fare clic su "Crea una nuova cartella".  
c. Fare clic su "OK" e quindi "estrarre", per estrarre i file.  
  
5. **Aprire cmd.exe**  
  
6. **Inizializzare Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Installare la Gemma TinyTDS**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Apri terminale**  
  
2. **Installare Ruby Version Manager (rvm) e i prerequisiti**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Usare rvm per installare Ruby**  
Ad esempio, installare la versione 2.3.0 di Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Assicurarsi che l'output dell'ultimo comando indichi che si esegue la versione 2.3.0.  
  
4.  **Installare FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Installare TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Si noti che Mac OS X ha già Ruby pre-installati, come il sistema operativo ha una dipendenza.    
  
1.  **Apri terminale**  
  
2. **Installare Gestione pacchetti Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Installare FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Installare la Gemma TinyTDS**  
```  
> gem install tiny_tds  
```
