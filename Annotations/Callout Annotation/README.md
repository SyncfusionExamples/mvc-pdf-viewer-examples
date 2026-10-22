# Callout Annotation in ASP.NET MVC PDF Viewer

This sample demonstrates how to enable, add, customize, and manage **Callout annotations** in the ASP.NET MVC PDF Viewer using the Syncfusion EJ2 PDF Viewer component. Callout annotations let users place an editable text box on a PDF page and connect it to a target point with one or more callout leader lines — ideal for review notes, labels, and call-outs that reference specific areas of a document without altering the original content.

## What is covered

- Enabling Callout annotations in the PDF Viewer.
- Switching to Callout Annotation mode programmatically (`annotation.setAnnotationMode('Callout')`).
- Exiting Callout Annotation mode (`annotation.setAnnotationMode('None')`).
- Adding a Callout annotation programmatically with `annotation.addAnnotation('Callout', { ... })`, including:
  - `offset`, `pageNumber`
  - `calloutLines` (the ordered leader-line path)
  - `lineEndingStyle`, `borderColor`, `borderWidth`, `borderStyle`
  - `opacity`, `author`
- Editing an existing Callout annotation programmatically.

## Run the sample

1. Open the `CalloutAnnotation.csproj` in Visual Studio.
2. Restore NuGet packages.
3. Build and run the project.

## Learn more

Refer to the Syncfusion UG documentation for the ASP.NET MVC PDF Viewer:

`https://help.syncfusion.com/document-processing/pdf/pdf-viewer/asp-net-mvc/getting-started`