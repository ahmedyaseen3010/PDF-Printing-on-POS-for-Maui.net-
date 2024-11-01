<H1>📄 PDF Printing on POS for .NET MAUI</H1>
<h2>Overview</h2>
.NET MAUI currently lacks a built-in API for printing documents like PDFs or HTML directly. This repository presents a work around solution for handling PDF printing on POS devices using .NET MAUI.
<h2>🛠️ Solution</h2>
Instead of printing documents directly through your app, you can install a printing service on your POS device. In this example, the RawBT Print Service is utilized, which can be downloaded from the POS device's app store.

To manage PDF files within the app, the Aspose.Pdf library is used, providing powerful PDF handling features for .NET environments. More information can be found in the Aspose.Pdf Documentation. 
https://docs.aspose.com/pdf/net/

<h2>🚀 How It Works</h2>
Install a Printing Service: Download and install the "RawBT Print Service" (or any suitable service) from your POS app store. <br/>
link: https://apkpure.com/rawbt-print-service/ru.a402d.rawbtprinter/download .<br/>
Integrate Aspose.Pdf: Use the Aspose.Pdf library in your project to manage and manipulate PDF files.<br/>
Print PDFs: once you click on the button, it should ask you about which app you want to open your file with, so choose the printing service that you installed.<br/>
Printer : once you choose the service it will automatically print this PDF 

![Alt text](https://drive.google.com/uc?id=14zyqoM3Y_24ww_mG4lWrY8YXM46vJXz1)



<h2>📋 Code Sample</h2>

using Aspose.Pdf.Facades;
using System;
using System.IO;               
using Microsoft.Maui.Controls;  
namespace osMauiTaxAgent;
public partial class NewPagePrint : ContentPage
{
    public NewPagePrint()
    {
        InitializeComponent();
    }

    private void Button_Clicked(object sender, EventArgs e)
    {
        var pdfFileName = "/storage/emulated/0/Android/data/com.COMPANYNAME.PROJECTNAME/settings/test1.pdf";

        if (File.Exists(pdfFileName))
        {
            try
            {
                using (Stream pdfStream = File.OpenRead(pdfFileName))
                {
                    var pdfViewer = new PdfViewer();
                    pdfViewer.OpenPdfFile(pdfStream);
                }
            }
            catch (Aspose.Pdf.InvalidPdfFileFormatException ex)
            {
                DisplayAlert("Error", $"Invalid PDF file format: {ex.Message}", "OK");
            }
            catch (Exception ex)
            {
                DisplayAlert("Error", $"An error occurred: {ex.Message}", "OK");
            }
        }
        else
        {
            DisplayAlert("Error", "PDF file not found.", "OK");
        }
    }
}
