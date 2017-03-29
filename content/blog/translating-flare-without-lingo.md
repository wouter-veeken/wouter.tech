+++
title = "Translating a MadCap Flare project without Lingo"
description = ""
tags = [
    "madcap",
    "flare",
    "lingo",
    "rainbow",
    "okapi"
]
date = "2017-03-24"
categories = [
    "l10n",
    "tutorials"
]
highlight = "true"
+++

I don't really like MadCap Lingo. Compared to other modern, more mature CAT tools, I have found it buggy and primitive, not to mention expensive for what it does. So when I needed to get my MadCap Flare project translated into 4 different languages, I set out to find a way of doing it that didn't require Lingo. I am sharing my findings for the benefit of those looking to achieve something similar.

**DISCLAIMER**: The below has worked for me – so far. My translations are still ongoing. It's entirely possible that 1) my methods don't work for your project and 2) I run into problems with my own project later on. Nevertheless, I am hoping this will get you at least part of the way there. You're always welcome to [ask me questions](mailto:me@wouter.tech) if you think I can help.

## What you'll need

* Some knowledge of HTML, XML and similar markup languages;
* a MadCap Flare project;
* Rainbow, which is bundled with the [Okapi Framework apps](https://bintray.com/okapi/Distribution/Okapi_Applications).

In addition, it helps if you have:

* a basic understanding of translation processes and related file types, such as TMX and XLIFF;
* [OmegaT](http://www.omegat.org/en/omegat.html), to test the translation package you're creating.

## Terms and acronyms used in this article

- **LSP:** Language service provider, e.g. a translation agency.
- **CAT tool:** Computer assisted translation tool, e.g. Trados, MemoQ and similar.

## Translating the project vs. translating the output

There are essentially two ways you can approach the translation of your Flare project: you can either translate your original project files (pre-build), or you can translate the actual output (post-build). My process uses the first approach, but here are some pros and cons for both options:

Translating the project:

- [+] Everything is nicely compartmentalized, i.e. variables, snippets, TOC, topics are in separate files.
- [+] Can extract image annotations for translation (if you're using Capture).
- [-] Can't use condition tags to exclude files you don't want to translate.
- [-] Since you have to build the project after putting the files through multiple conversion and translation steps, there might be some surprises.

Translating the output:

- [+] Project is already built, so the risk of breaking stuff by converting/translating files is much smaller.
-  [+] Can use condition tags to exclude files from translation.
- [-] Translation package will contain lots of repetition (e.g. snippets, the same TOC on every page), which is annoying for translator and may affect translation cost.
- [-] Can't extract image annotations for translation.

Although there are several reasons why I chose the first approach, that last one cinched it for me. If image annotations are not a factor for you, perhaps it might be easier to just zip the output and send it off to your translator or LSP.

## High-level steps

Here's what you'll roughly be doing if you follow my instructions:

1. Export a copy of your source-language project from Flare.
2. Add the files you want to translate to Rainbow.
3. Create a few custom filter configurations in Rainbow.
4. Create a translation package in Rainbow.
5. Send everything to be translated.
6. Convert the translated files back to their original format in Rainbow.
7. Build the translated project in Flare.

This is just to provide an overview. It is not a table of contents.

## Preparing your project for translation

Open your project in Flare and select **Project > Export Project** to create a copy. I recommend appending the filename with the source and target language codes, e.g. `my_flare_project_en-US_fr-FR.flprj` if you're translating from (US) English to French.

## Preparing your translation package with Rainbow

Rainbow is sort of a Swiss army knife for translators and translation project managers. It offers file conversion, terminology extraction, quality checks, pre-translation, and about a million other things I haven't even begun to explore myself. Unfortunately, it's also got a steep learning curve. There's a [wiki](http://okapiframework.org/wiki/index.php?title=Rainbow) which is fairly comprehensive, but it often lacks detail in important areas, and some parts seem out of date. Thankfully, you've got this blog to help you!

### Basic configuration

Fire up Rainbow and do these things:

1. On the **Languages and Encodings** tab, select the relevant source and target language.
2. On the same tab, set the encoding for source and target to **Unicode (UTF-8)**.

    **NOTE**: This was the correct encoding for my project files – I assume it's the same for all Flare projects. You can check by opening one of your topics in a program like [Notepad++](https://notepad-plus-plus.org/).
3. On the **Other Settings** tab, de-select **Use an extension**. This is important because you want the final, translated files to retain their original names. Under the default settings, `topic.htm` becomes `topic.out.htm`.
4. Save your configuration (**File > Save**).

### Adding files to your package

1. Select the **Input List 1** tab.
2. In Windows Explorer, navigate to the root directory of your exported Flare project.
3. Drag all the file types you want to translate into the Rainbow window. (See [Which files to include](#WhichFilesToInclude) below.)
4. Delete from the list any files you don't want translated. You could do this by opening your Flare projects and looking for files with certain publishing conditions or file tags (e.g. 'draft', 'internal only').

#### <a name="WhichFilesToInclude"></a>Which files to include

From the `Project` folder:

* Glossaries (`.flglo`)
* TOCs (`.fltoc`)
* VariableSets (`.flvar`)

From the `Content` folder:

* MasterPages (`.flmsp`)
* Image properties (`.props`)
* PageLayouts (`.flpgl`)
* Snippets (`.flsnp`)
* Topics (`.htm`)

Files I have not tried to translate, as my project doesn't use them:

* `Project\Synonyms`
* `Project\CSH`
* `Project\Browse sequences`

Files that need special treatment (will cover this in a future update – ignore them for now):

* `Content\Stylesheets`

### Creating custom filters

Rainbow includes a large set of filter configurations, which you can see by selecting **Tools > Filter Configurations**. Rainbow uses these filters to  determine which parts of a given file are translatable, i.e. which parts it should extract and put in a translation package.

A Flare project consists of HTML and XML files, and Rainbow will automatically apply the **okf_html** and **okf_xml** filters when you add such files to the input list (see the **Filter Configuration** column). For glossaries (`.flglo`) and variable sets (`.flvar`), the default **okf_xml** filter works fine, but the other file types require a little more work: we'll need to create custom filters for them.

#### Create filter for topics (`.htm`), snippets (`.flsnp`) and master pages (`.flmsp`)

1. Using your mouse and the **Ctrl** and **Shift** keys, select all files ending in `.htm`, `.flsnp` or `.flmsp`.
2. Right-click on any of the selected files and select **Edit Document Properties**.
The **okf_html** filter will be selected.
3. Click **Create** to create a custom filter configuration based on **okf_html**.
4. Enter the name `flare-topic` and click **OK**. The full name will appear as `okf_html@flare-topic`.
The filter's parameters appear. This particular filter uses the [YAML](https://en.wikipedia.org/wiki/YAML) format.
5. Change `preserve_whitespace: false` to `true`. This ensures that the whitespace around e.g. cross-references is retained during conversion.
6. Scroll down a little until you see `elements:` and insert the following lines immediately after it:

    ```yaml
    madcap:variable:
      ruleTypes: [INLINE]
      SelementType: variable    
    ```

    This ensures proper handling of in-line variables. (They are treated as line breaks otherwise.)

7. Click **OK** to close the editor, then **OK** to return to the file list.
8. Now is probably a good time to save your Rainbow configuration file, so select **File > Save**.

#### Create filter for TOCs (`.fltoc`)

1. Using the same methods as above, select all `.fltoc` files and create a new filter called `okf_xml@flare-TOC`.
Unsurprisingly, the parameters of this filter are written in XML.
2. Replace the default parameters with the following:

    ```xml
    <?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <its:rules xmlns:its="http://www.w3.org/2005/11/its" xmlns:itsx="http://www.w3.org/2008/12/its-extensions" xmlns:okp="okapi-framework:xmlfilter-options" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.0">
      <its:translateRule selector="//@Title" translate="yes"/>
      <!-- See ITS specification at: http://www.w3.org/TR/its/ -->
    </its:rules>
    ```

This tells Rainbow that the values of all `Title` attributes contain translatable text. (By default, all attributes are considered non-translatable.)

#### Create filter for image annotations (`.props`)

1. Select all `.props` files and create a new filter called `okf_xml@flare-props`, containing this code:

    ```xml
    <?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <its:rules xmlns:its="http://www.w3.org/2005/11/its" xmlns:itsx="http://www.w3.org/2008/12/its-extensions" xmlns:okp="okapi-framework:xmlfilter-options" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.0">
      <its:translateRule selector="//fileProperties" translate="no"/>
      <its:translateRule selector="//Shape[@Type='Annotation']" translate="yes"/>
      <!-- See ITS specification at: http://www.w3.org/TR/its/ -->
    </its:rules>
    ```

This tells rainbow that all `<fileProperties>` elements _and_ their children should be ignored, _except_ when one of those children is a `<Shape Type='Annotation'>`.

### Save your filters for future use

It's a good idea to back up your custom filters for future translation projects. By default, they are stored in Rainbow's installation directory, in a subfolder called `config`. You can keep them there, or organize them by project/client/category/whatever.

### Create the translation package

Rainbow lets you create conversion 'pipelines' that allow you to put in a bunch of files on one end (i.e. source texts, terminology files, translation memories) and get a neat little translation package at the other, that you can then send off to a translator/LSP. You can build these pipelines from scratch by using dozens of configurable steps, but Rainbow also comes with a couple of pre-defined pipelines, which you'll be using.

1. Select **Utilities > Translation Kit Creation**.
This fires up the pre-defined pipeline for creating translation packages.
2. In the list of steps on the left, select the bottom one (**Rainbow TRanslation Kit Creation**).
3. On the **Package Format** tab, select **Generic XLIFF**.
**NOTE:** Any CAT tool worth its salt (e.g. Trados, MemoQ, OmegaT) can handle [XLIFF](https://en.wikipedia.org/wiki/XLIFF), so that's what I use. But you can theoretically use any of the other formats as well – you just won't be able to use my instructions from hereon.
4. Click **Options** and make sure these options are selected (they might be by default, I'm not sure):
    * **Use \<g>\</g> and \<x/> notation**
    * **Copy source text in target if no target is available**
5. On the **Output Location** tab, choose an output folder and give the package a name. I recommend mentioning the source and target language in both.
6. Optionally, add any translation memories, terminology files and other supporting documents on the **Support Material** tab.
7. When you're ready, click **Execute**.
   Rainbow now goes through each file, extracts translatable text based on your filter configurations, splits that text into segments (i.e. sentences) and stores it all in XLIFF (`.xlf`) files. There will be one XLIFF file for each source file.
   Note that the log may contain some alarming lines like `Trying to end a TextUnit that does not exist`. Don't worry: as long as the error and warning counts at the bottom are both at 0, everything went fine.

If everything goes well, your output folder will contain these things:

* A folder called `original`, which contains the original source files (for the translator's reference).
* A folder called `work`, which contains all the translatable `.xlf` files.
* A file called `manifest.rkm`, which contains information about where each individual translatable text came from. Rainbow uses this to determine where to insert the translations as it converts the translated files back to their original formats.

If you want, you can get an idea of how your files will look like to the translator by opening them in [OmegaT](http://www.omegat.org/en/omegat.html).

## Translating the project files

### Sending the package to your translator

As I mentioned earlier, any serious CAT tool should be able to handle XLIFF files. By the same token, so should any serious translator. If your translator says they can't, find another translator.

You can email the files in a zip file, host them on Dropbox, or transfer them any other way you want. It doesn't really matter, as long as:

* you get the translated files back in `.xlf` format;
* the original folder structure of the `work` folder is kept intact;
* the `manifest.rkm` file is not tampered with.

Regarding that last point: I recommend not even sending it. It's vital for you, but the translator has no use for it.

### Processing the package after translation

If everything went as it should, the translator should send you back the same basic set of files, with the same folder structure, except all the `.xlf` files have been modified. You can open them with a text editor and see that each source segment now has a matching translation. You're now going to run these files through Rainbow again to convert them back to their original format.

1. In Rainbow, create a new configuration file (**File > New**).
**NOTE:** If you're like me, you'd expect to load up your previous configuration and continue where you left off. But that's not how Rainbow works – you really do need a fresh config.
2. Drag the `manifest.rkm` file into the file list.
3. Select **Utilities > Translation Kit Post-Processing**. This loads up another pre-defined pipeline that more or less does the reverse of the one you used previously.
4. Click **Execute**. You'll see an overview of all the files that are going to be post-processed.
5. Click **Continue**.

The converted, translated files will be in a folder called `done`, on the same level als the `original` and `work` folders.

## Building the translated project

Copy the translated files into your project folder. Build the project. Done!

<!--
## Translating subsequent updates

How to handle updates after the bulk is published? Just send out entire project again with TM included? Could work I guess.
-->
