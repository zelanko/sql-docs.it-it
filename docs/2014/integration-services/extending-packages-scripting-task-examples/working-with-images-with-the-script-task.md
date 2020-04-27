---
title: Uso di immagini con l'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b27b5bbc77d1d48e3697893e2e21dcf7d8a6c570
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62768447"
---
# <a name="working-with-images-with-the-script-task"></a>Utilizzo di immagini con l'attività Script
  Un database di prodotti o utenti include di frequente immagini oltre a testo e dati numerici. Lo spazio dei nomi `System.Drawing` in Microsoft .NET Framework fornisce le classi per la modifica delle immagini.  
  
 [Esempio 1: convertire immagini in formato JPEG](#example1)  
  
 [Esempio 2: creare e salvare le immagini di anteprima](#example2)  
  
> [!NOTE]  
>  Se si desidera creare un'attività da riutilizzare più facilmente con più pacchetti, è possibile utilizzare il codice di questo esempio di attività Script come punto iniziale per un'attività personalizzata. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
##  <a name="example-1-description-convert-images-to-jpeg-format"></a><a name="example1"></a> Descrizione dell'esempio 1: convertire immagini in formato JPEG  
 Nell'esempio seguente viene aperto un file di immagine specificato da una variabile e lo salva come file JPEG compresso tramite un codificatore. Il codice per recuperare le informazioni sul codificatore viene incapsulato in una funzione privata.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Per configurare questa attività Script di esempio per l'utilizzo con un solo file di immagine  
  
1.  Creare una variabile di stringa denominata `CurrentImageFile` e impostarne il valore sul percorso e sul nome di un file di immagine esistente.  
  
2.  Nella pagina **script** dell' **Editor attività script**aggiungere la `CurrentImageFile` variabile alla `ReadOnlyVariables` proprietà.  
  
3.  Nel progetto di script impostare un riferimento allo spazio dei nomi `System.Drawing`.  
  
4.  Nel codice utilizzare le istruzioni `Imports` per importare gli spazi dei nomi `System.Drawing` e `System.IO`.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Per configurare questa attività Script di esempio per l'utilizzo con più file di immagine  
  
1.  Inserire l'attività Script all'interno di un contenitore Ciclo Foreach.  
  
2.  Nella pagina **Raccolta** dell'**Editor ciclo Foreach** selezionare **Enumeratore Foreach File** come enumeratore e specificare il percorso e il filtro dei file di origine, ad esempio "*.bmp".  
  
3.  Nella pagina **Mapping variabili** eseguire il mapping della variabile `CurrentImageFile` all'indice 0. Questa variabile passa il nome file corrente all'attività Script a ogni iterazione dell'enumeratore.  
  
    > [!NOTE]  
    >  Questi passaggi vengono aggiunti a quelli elencati nella procedura per l'utilizzo con un solo file di immagine.  
  
### <a name="example-1-code"></a>Codice dell'esempio 1  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example-2-description-create-and-save-thumbnail-images"></a><a name="example2"></a> Descrizione dell'esempio 2: creare e salvare le immagini di anteprima  
 Nell'esempio seguente viene aperto un file di immagine specificato da una variabile, viene creata un'anteprima dell'immagine pur mantenendo una proporzione costante e viene salvata l'anteprima con un nome file modificato. Il codice che calcola l'altezza e larghezza dell'anteprima mantenendo una proporzione costante viene incapsulato in una subroutine privata.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>Per configurare questa attività Script di esempio per l'utilizzo con un solo file di immagine  
  
1.  Creare una variabile di stringa denominata `CurrentImageFile` e impostarne il valore sul percorso e sul nome di un file di immagine esistente.  
  
2.  Creare anche la variabile di tipo integer `MaxThumbSize` e assegnare un valore in pixel, ad esempio 100.  
  
3.  Nella pagina **script** dell' **Editor attività script**aggiungere entrambe le `ReadOnlyVariables` variabili alla proprietà.  
  
4.  Nel progetto di script impostare un riferimento allo spazio dei nomi `System.Drawing`.  
  
5.  Nel codice utilizzare le istruzioni `Imports` per importare gli spazi dei nomi `System.Drawing` e `System.IO`.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>Per configurare questa attività Script di esempio per l'utilizzo con più file di immagine  
  
1.  Inserire l'attività Script all'interno di un contenitore Ciclo Foreach.  
  
2.  Nella pagina **Raccolta** dell'**Editor ciclo Foreach** selezionare **Enumeratore Foreach File** come **enumeratore** e specificare il percorso e il filtro dei file di origine, ad esempio "*.jpg".  
  
3.  Nella pagina **Mapping variabili** eseguire il mapping della variabile `CurrentImageFile` all'indice 0. Questa variabile passa il nome file corrente all'attività Script a ogni iterazione dell'enumeratore.  
  
    > [!NOTE]  
    >  Questi passaggi vengono aggiunti a quelli elencati nella procedura per l'utilizzo con un solo file di immagine.  
  
### <a name="example-2-code"></a>Codice dell'esempio 2  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
![Integration Services icona (piccola)](../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
  
