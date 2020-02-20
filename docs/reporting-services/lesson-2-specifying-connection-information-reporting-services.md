---
title: 'Lezione 2: Specificare le informazioni di connessione (Reporting Services) | Microsoft Docs'
description: In questa lezione si definisce un'origine dati, ovvero si specificano le informazioni di connessione usate dal report per accedere ai dati di un database relazionale o altre origini.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9d4e12a0322a35e96bd930c4fa6f1f852daf2bdd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75258458"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lezione 2: Definizione delle informazioni di connessione (Reporting Services)

Nella lezione 1 è stato aggiunto un report impaginato [!INCLUDE[ssrsnoversion-md](../includes/ssrsnoversion-md.md)] al progetto Tutorial.
  
In questa lezione si definirà un'*origine dati*, ovvero si specificheranno le informazioni di connessione usate dal report per accedere ai dati di un database relazionale o altre origini.

Per questo report si aggiungerà il database di esempio AdventureWorks2016 come origine dati. Questa esercitazione presuppone che il database si trovi nell'istanza predefinita del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] e che sia installato nel computer locale.  

## <a name="to-set-up-a-connection"></a>Per impostare una connessione  

1. Nel riquadro **Dati report** selezionare **Nuovo** > **Origine dati**. Se il riquadro **Dati report** non è visibile, scegliere **Dati report** dal menu **Visualizza**.

    ![ssrs-table-tutorial-2-new-data-source](media/ssrs-table-tutorial-2-new-data-source.png)

    Verrà visualizzata la sezione **Generale** della finestra di dialogo **Proprietà origine dati**.

    ![Finestra di dialogo Proprietà origine dati](media/lesson-2-specifying-connection-information-reporting-services/vs-datasource-connection-properties-dialog-box.png)

2. Nella casella di testo **Nome** digitare "AdventureWorks2016".

3. Selezionare il pulsante di opzione **Connessione incorporata**.

4. Nella casella di selezione a discesa **Tipo** selezionare "Microsoft SQL Server".
  
5. Nella casella di testo **Stringa di connessione** digitare la stringa seguente:

    `Data source=localhost; initial catalog=AdventureWorks2016`

    > [!NOTE]
    > Questa stringa di connessione presuppone che [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], il server di report e il database AdventureWorks2016 siano tutti installati nel computer locale.
    >
    >Se non lo sono, modificare la stringa di connessione e sostituire "localhost" con il nome dell'istanza o del server di database. Se si usa [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] o un'istanza denominata di SQL Server, è necessario modificare la stringa di connessione in modo da includere le informazioni relative all'istanza. Ad esempio:
    >
    > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2016`
    >
    > Per altre informazioni sulle stringhe di connessione, vedere la sezione `See also` riportata di seguito.

6. Selezionare la scheda **Credenziali** e quindi il pulsante di opzione **Usa autenticazione di Windows (sicurezza integrata)** nella sezione **Modificare le credenziali utilizzate per connettersi all'origine dati**.

7. Selezionare **OK** per completare il processo.

Progettazione report aggiungerà l'origine dati AdventureWorks2016 al riquadro **Dati report**.

![ssrs-adventureworks-datasource](media/lesson-2-specifying-connection-information-reporting-services/ssrs-adventureworks-datasource2016.png)

## <a name="next-steps"></a>Passaggi successivi

In questa lezione è stata definita una connessione al database di esempio AdventureWorks2016. Procedere a [Lezione 3: Definizione di un set di dati per il report tabella &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md) per definire un set di dati per il report.

## <a name="see-also"></a>Vedere anche

[Creare stringhe di connessione dati - Generatore report e SSRS](report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)
