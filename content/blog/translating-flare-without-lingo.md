+++
date = "2017-03-24"
title = "Translating a MadCap Flare project without Lingo"
description = "Tutorial for creating a translation package from a MadCap Flare project with the open source tool Rainbow"
draft = "false"
highlight = "true"
tags = [
    "madcap",
    "flare",
    "lingo",
    "rainbow",
    "okapi"
]
categories = [
    "l10n",
    "tutorials"
]
+++

For reasons I won't go into, I'm not a fan of MadCap Lingo. So when I needed to get my MadCap Flare project translated into 4 different languages, I came up with an alternative solution using an open source tool called [Rainbow][okapi]. I am sharing my approach here for the benefit of others.

**DISCLAIMER**: The below has worked for me – so far. My translations are still ongoing. It's entirely possible that 1) my methods don't work for your project and 2) I run into problems with my own project later on. Nevertheless, I am hoping this will get you at least part of the way there. You're always welcome to [ask me questions][email] if you think I can help.

## What you'll need

* Some knowledge of HTML, XML and similar markup languages;
* a MadCap Flare project;
* Rainbow, which is bundled with the [Okapi Framework apps][okapi]

    **NOTE:** Some people have reported problems running the 64-bit version of Rainbow. If that's the case for you, install the 32-bit version. It works exactly the same.  

In addition to the above, it helps if you have:

* a basic understanding of translation processes and related file types, such as TMX and XLIFF;
* [OmegaT][omegat], to test the translation package you're creating.

## Terms and acronyms used in this article

- **LSP:** Language service provider, e.g. a translation agency.
- **CAT tool:** Computer assisted translation tool, e.g. Trados, MemoQ and similar.

## Translating the project vs. translating the output

You can approach the translation of your Flare project in two ways. You can either translate your original project files (pre-build), or you can translate the actual output (post-build). My process uses the first approach, but here are some pros and cons for both options:

Translating the project:

- [+] Everything is nicely compartmentalized, i.e. variables, snippets, TOC, topics are in separate files.
- [+] Can extract image annotations for translation (if you're using Capture).
- ~~[-] Can't use condition tags to exclude files you don't want to translate.~~
    **EDIT 03-Apr-2017**: I totally failed to notice that you can choose include/exclude conditions when you <a href="#PreparingYourProjectForTranslation">export the project from Flare</a>. So this isn't a con at all!
- [-] Since you have to build the project after putting the files through multiple conversion and translation steps, there might be some surprises.

Translating the output:

- [+] Project is already built, so the risk of breaking stuff by converting/translating files is much smaller.
- [-] Translation package will contain lots of repetition (e.g. snippets, the same TOC on every page), which is annoying for translator and may affect translation cost.
- [-] Can't extract image annotations for translation.

Although there are several reasons why I chose the first approach, that last one clinched it for me. If image annotations are not a factor for you, perhaps it might be easier to just zip the output and send it off to your translator or LSP.

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

## <a name="PreparingYourProjectForTranslation"></a>Part 1 of 4: Preparing your project for translation

1. Open your project in Flare and select **Project > Export Project** to create a copy. Tips:

    * Select **Export From** > **Using Conditions** to exclude drafts and other files you don't want translated.

        **NOTE:** You could use a special condition tag to explicitly mark files for translation, but make sure you export all the files you need to be able to build the project at the end.

    * I recommend appending the filename of the exported project with the source and target language codes. E.g. if you're translating from (US) English to French, save as `my_flare_project_en-US_fr-FR.flprj`.
2. Open the exported project and select **Project > Project Properties**.
3. Under **Language**, select the target language. This should take care of any translatable labels in your project skins (e.g. search box place holder, topic toolbar buttons), provided that 1) Flare has default translations for the chosen language and 2) you have configured your skins to use the default project language.

## Part 2 of 4: Preparing your translation package with Rainbow

Rainbow is sort of a Swiss army knife for translators and translation project managers. It offers file conversion, terminology extraction, quality checks, pre-translation, and about a million other things I haven't even begun to explore myself. Unfortunately, it's also got a steep learning curve. There's a [wiki][rainbow-wiki] which is fairly comprehensive, but it often lacks detail in important areas, and some parts seem out of date. Thankfully, you've got this blog to help you!

### Basic configuration

Fire up Rainbow and do these things:

1. On the **Languages and Encodings** tab, select the relevant source and target language.
2. On the same tab, set the encoding for source and target to **Unicode (UTF-8)**.

    **NOTE**: This was the correct encoding for my project files – I assume it's the same for all Flare projects. You can check by opening one of your topics in a program like [Notepad++][notepad++].

3. On the **Other Settings** tab, de-select **Use an extension**. This is important because you want the final, translated files to retain their original names. Under the default settings, `topic.htm` becomes `topic.out.htm`.
4. Save your configuration (**File > Save**).

### Adding files to your package

1. Select the **Input List 1** tab.
2. In Windows Explorer, navigate to the root directory of your exported Flare project.
3. Drag all the file types you want to translate into the Rainbow window. (See [Which files to include](#WhichFilesToInclude) below.)
4. Delete from the list any files you don't want translated. You could do this by opening your Flare projects and looking for files with certain publishing conditions or file tags (e.g. 'draft', 'internal only').

#### <a name="WhichFilesToInclude"></a>Which files to include

From the `Project` folder:

* `Project\Glossaries` (`.flglo`)
* `Project\TOCs` (`.fltoc`)
* `Project\VariableSets` (`.flvar`)

From the `Content` folder:

* `Content\MasterPages` (`.flmsp`)
* `Content\PageLayouts` (`.flpgl`)
* All image property files (`.props`)
* All snippet files (`.flsnp`)
* All topic files (`.htm`)

Files I have not tried to translate, as my project doesn't use them:

* `Project\Synonyms`
* `Project\CSH`
* `Project\Browse sequences`

Files that need special treatment (will cover this in a future update – ignore them for now):

* `Content\Stylesheets`

### Applying filters

Rainbow includes a large set of filter configurations, which you can see by selecting **Tools > Filter Configurations**. Rainbow uses these filters to  determine which parts of a given file are translatable, i.e. which parts it should extract and put in a translation package.

A Flare project consists of HTML and XML files. Rainbow has default filters for these file types, but they will only work for a few of your files. You'll have to create custom filters for the rest.

#### Apply default filter to glossaries (`.flglo`) and variable sets (`.flvar`)

The default **okf_xml** filter will work for glossaries and variable sets. To apply this filter:

1. Using your mouse and the **Ctrl** and **Shift** keys, select all files ending in `.flglo` and `.flvar`.
2. Right-click on any of the selected files and select **Edit Document Properties**.
3. Under **Filter configuration**, select **XML Filter**.

    ![Select the XML filter](/img/rainbow-select-xml-filter.png)

4. Click **OK**.

In the **Filter Configuration** column, it should say **okf_xml**.

#### Create filter for topics (`.htm`), snippets (`.flsnp`) and master pages (`.flmsp`)

1. Using the same methods as above, select all files ending in `.htm`, `.flsnp` and `.flmsp`.
2. Right-click on any of the selected files and select **Edit Document Properties**.
3. Under **Filter configuration** select **HTML/XHTML Filter**.
4. Click **Create** to create a custom filter configuration based on **okf_html**.

    ![Create a custom filter](/img/rainbow-create-custom-filter.png)

4. Enter the name `flare-topic` and click **OK**. The full name will appear as `okf_html@flare-topic`.

    The filter's parameters now appear. This particular filter uses the [YAML][wikipedia-yaml] format.

    ![HTML filter parameters](/img/rainbow-html-filter-parameters.png)

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

1. Select all `.fltoc` files and create a new filter called `okf_xml@flare-TOC`.

    Unsurprisingly, the parameters of this filter are written in XML.

    ![XML filter parameters](/img/rainbow-xml-filter-parameters.png)

2. Replace the default parameters with the following:

    ```xml
    <?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <its:rules xmlns:its="http://www.w3.org/2005/11/its" xmlns:itsx="http://www.w3.org/2008/12/its-extensions" xmlns:okp="okapi-framework:xmlfilter-options" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.0">
      <its:translateRule selector="//@Title" translate="yes"/>
      <!-- See ITS specification at: http://www.w3.org/TR/its/ -->
    </its:rules>
    ```

This tells Rainbow that the values of all `Title` attributes contain translatable text. (By default, attributes in XML files are considered non-translatable.)

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

#### Save your filters for future use

It's a good idea to back up your custom filters for future translation projects. By default, they are stored in Rainbow's installation directory, in a subfolder called `config`. You can keep them there, or organize them by project/client/category/whatever.

### Create the translation package

A fundamental feature of Rainbow is that it lets you build conversion 'pipelines', which enable you to put in a bunch of files on one end (i.e. source texts, terminology files, translation memories) and produce a neat little translation package at the other, which you can then send off to a translator/LSP.

You can build your pipelines from scratch by choosing from dozens of configurable steps, but for the present purposes you can use one of Rainbow's pre-defined pipelines.

1. Select **Utilities > Translation Kit Creation**.
This fires up the pre-defined pipeline for creating translation packages.

    ![Translation Kit Creation pipeline](/img/rainbow-translation-kit-creation.png)

2. In the list of steps on the left, select the bottom one (**Rainbow Translation Kit Creation**).
3. On the **Package Format** tab, select **Generic XLIFF**.

    **NOTE:** Any CAT tool worth its salt (e.g. Trados, MemoQ, OmegaT) can handle [XLIFF][wikipedia-xliff], so that's the format I use. But you can theoretically use any of the other formats as well – you just won't be able to use my instructions from hereon.

4. Click **Options** and make sure these options are selected (they might be by default, I'm not sure):
    * **Use \<g>\</g> and \<x/> notation**
    * **Copy source text in target if no target is available**
5. On the **Output Location** tab, choose an output folder and give the package a name. I recommend mentioning the source and target language in both.
6. Optionally, add any translation memories, terminology files and other supporting documents on the **Support Material** tab.
7. When you're ready, click **Execute**.

    Rainbow now goes through each file, extracts translatable text based on your filter configurations, splits that text into segments (i.e. sentences) and stores it all in XLIFF (`.xlf`) files. There will be one XLIFF file for each source file.

    Don't worry if the log contains mildly alarming messages like `Trying to end a TextUnit that does not exist`. As long as the error and warning counts at the bottom are both at 0, everything is fine.

If things went as they should, your output folder will contain these things:

* A folder called `original`, which contains the original source files (for the translator's reference).
* A folder called `work`, which contains all the translatable `.xlf` files.
* A file called `manifest.rkm`, which contains information about where each individual translatable text came from. Rainbow uses this to determine where to insert the translations as it converts the translated files back to their original formats.

If you want, you can open your files in [OmegaT][omegat] to see how they look for the translator.

## Part 3 of 4: Translating the project files

### Sending the package to your translator

As I mentioned earlier, any serious CAT tool should be able to handle XLIFF files. By the same token, so should any serious translator. If your translator says they can't work with XLIFF, find another translator.

You can email the files in a zip file, host them on Dropbox, or transfer them any other way you want. It doesn't really matter, as long as:

* you get the translated files back in `.xlf` format;
* the original folder structure of the `work` folder is kept intact;
* the `manifest.rkm` file is not tampered with.

In fact, I recommend not even sending the manifest file. The translator has no use for it.

### Processing the package after translation

If everything went as it should, the translator should send you back the same basic set of files, with the same folder structure, except all the `.xlf` files have been modified. You can open them with a text editor and see that each source segment now has a matching translation. You're now going to run these files through Rainbow again to convert them back to their original format.

1. In Rainbow, create a new configuration file (**File > New**).

    **NOTE:** If you're like me, you'd expect to load up your previous configuration and continue where you left off. But that's not how Rainbow works – you really do need a fresh config.

2. Drag the `manifest.rkm` file into the file list.
3. Select **Utilities > Translation Kit Post-Processing**. This loads up another pre-defined pipeline that more or less does the reverse of the one you used previously.
4. Click **Execute**. You'll see an overview of all the files that are going to be post-processed.
5. Click **Continue**.

The converted, translated files will be in a folder called `done`, on the same level als the `original` and `work` folders.

## Part 4 of 4: Building the translated project

Copy the translated files into your target-language project folder. Build the project. Done!

<!--
## Translating subsequent updates

How to handle updates after the bulk is published? Just send out entire project again with TM included? Could work I guess.
-->

<!-- Links and references -->
[okapi]:https://bintray.com/okapi/Distribution/Okapi_Applications
[omegat]:http://www.omegat.org/en/omegat.html
[rainbow-wiki]:http://okapiframework.org/wiki/index.php?title=Rainbow
[wikipedia-yaml]:https://en.wikipedia.org/wiki/YAML
[wikipedia-xliff]:https://en.wikipedia.org/wiki/XLIFF
[notepad++]:https://notepad-plus-plus.org/
[email]:mailto:me@wouter.tech
