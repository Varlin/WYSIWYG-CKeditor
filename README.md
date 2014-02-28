WYSIWYG-CKeditor
===
Modified extension of MediaWiki: WYSIWYG. Includes extension and other related modifed components.
Files of this bundle were originally taken from diffeent source bundles of extension WYSIWYG from MediaWiki site www.mediawiki.org.

You can find more information about MediaWiki extension WYSIWYG here:

  https://www.mediawiki.org/wiki/Extension:WYSIWYG
  https://www.mediawiki.org/wiki/Extension_talk:WYSIWYG

-----------
**NOTE!**

>  You will use this bundle in your environment at your own risk.  The authors of this package can not be held responsible for any issues this bundle may cause in your system.

-----------
**NOTE!**

>If you plan to use this bundle in your enviroment, requirement is that  you will give feedback and description of your environment and purpose  of your wiki here:
https://www.mediawiki.org/wiki/Extension_talk:WYSIWYG#Version_of_source_bundles_38239. If you are not willing to obey this humble request, then you may not use this bundle for any purposes.


----------
**You can find information about following issues below:**
- history of modifications (in reverse order)
- compatible Mediawiki environment
- short installation instructions
- compatible browsers and browser settings

================

------------
History of modifications:
===

- 28.02.14  Fixed height of texarea element in dialogs Tag, Template and Reference, because height of textarea does not grow when dialog is made higher.

- 27.02.14  Fixed finnish translation for header text of Tag -dialog. Fixed passing selection as text with IE in dialogs ref.js and category.js.

- 24.02.14  Problem with conflict page: changed "current page content" editing mode from wikieditor to wysiwyg. NOTE! Do not use refresh button of browser on conflict page, it corrupts contents of page in editor.

- 21.02.14  Problem with conflict page: section of "current contents of page" was using wysiwyg editor but text inside it was in wikitext mode => forced editor in wikitext mode (WikiEditor) in case of conflict (=two authors editing same page at same time, the one saving page as latest will get indication of conflict)

- 17.02.14  Fixed Tag -dialog (special.js) to support <source lang="xxx">. .<source> definition as "fck_mw_source" element (requires extension SyntaxHighlight_GeSHi). Errors found with IE11 native mode in wysiwyg editor: all dialogs work but they had focus problems with their respective elements on page, to fix this forced compatibility mode IE=9 with wysiwyg editing mode only. (WYSIWYG/CKeditor.body.php vs. includes/OutputPage.php)

- 14.02.14  IE11 works with wysiwyg in native mode (="Edge") as long as your wiki site IS NOT set to be viewed in compatibility mode with IE11.

- 12.02.14  Wysiwyg worked earlier with IE11 only in compatibility mode. Added code to enable wysiwyg mode in IE11 native mode.

- 10.02.14  Fixed two IE8 compatibility issues: tagged/numbered list emptied the page when saving page or changing into wikitext mode; ref.js dialog crashed, unable to save definition

- 06.02.14  Modified fix for IE 11 with Category.js

- 04.02.14  Tag -dialog (special.js) with variables of MW

- 03.02.14  Double clicking template image dialog (template.js)

- 17.01.14  WYSIWYG -editor together with WIkiEditor extension

- 10.01.14 <Ref> dialog: translations; image -dialog: width ja height values from image, resize image in edit mode

- 10.01.14  Category -button and dialog

- 09.01.14  Positions of [edit] link with headers

- 03.01.14  Ref, References -buttons

- 16.12.13  WYSIWYG_MV_v1.22.0.zip: WYSIWYG / IE11:n "numbered and bulleted" list; WYSIWYG / IE 11: Category -definition; IE11 html format 'IE=9' /opt/lampp/htdocs/mediawiki/includes/OutputPage.php

- 05.12.13  MW 1.21.2 => 1.22.0

- 10.11.13  MW 1.21.2, WYSIWYG_MW_v1.20.2.zip + manual fixes based on talk page of extension:wysiwyg

-----------------
**Origin of source bundles combined into this version:**

1. Version of WYSIWYG files were taken intially for MW 1.21 from here:
> https://docs.google.com/file/d/0B-aiZzKTmWI2bG8yVzBCOWNLamM/view?pli=1
> WYSIWYG_MW_v1.20.2.zip

2. Some modifications have been adapted into it from here:
>https://drive.google.com/file/d/0B-aiZzKTmWI2Q0wyd3FMRVpuZWM/view?pli=1
>WYSIWYG_MV_v1.22.0.zip

3. Some additinal features were developed based on this bundle
>http://wikirouge.net/nowiki/mediawiki/WYSIWYG

4. Additional features and modifications where applied on top of abowe bundles

========================

Short installation instructions:
===

----------------
**About MediaWiki environment:**

- MediaWiki:  1.21.2, 1.22.0, 1.22.1, 1.22.2
- PHP 5.5.6, MySQL 5.6.14, Apache 2.4.7 (XAMPP for Linux 1.8.3-2)

-----------------
**File: LocalSettings.php**

Make sure your LocalSettings.php has been set up properly, certain name spaces should be excluded from wysiwyg by default and some of the other settings should be in specific way for wysiwyg and wikieditor to work together:


    #13.11.13->
    require_once( "$IP/extensions/WYSIWYG/WYSIWYG.php" );

    #Or only for registered users:
    $wgGroupPermissions['registered_users']['wysiwyg']=true;
    $wgGroupPermissions['*']['wysiwyg'] = true;          //Everyone can use (if can edit)...
    $wgDefaultUserOptions['cke_show'] = 'richeditor';    //Enable CKEditor
    $wgDefaultUserOptions['riched_use_toggle'] = false;  //Editor can toggle CKEditor/WikiText
    $wgDefaultUserOptions['riched_start_disabled'] = false; //Important!!! else bug...
    $wgDefaultUserOptions['riched_toggle_remember_state'] = true; //working/bug?
    $wgDefaultUserOptions['riched_use_popup'] = false;   //Deprecated

    ##These are not compatible with WYSIWYG
    $wgFCKEditorExcludedNamespaces[] = NS_MEDIAWIKI;
    $wgFCKEditorExcludedNamespaces[] = NS_TEMPLATE;
    #13.11.13<-

    #17.01.14->
    #WikiEditor may not be compatible with WYSIWYG editor, use it with caution.
    require_once( "$IP/extensions/WikiEditor/WikiEditor.php" );

    # Enables/disables use of WikiEditor by default but still allow users to disable it in preferences
    $wgDefaultUserOptions['usebetatoolbar'] = 1;
    $wgDefaultUserOptions['usebetatoolbar-cgd'] = 1;

    # Displays the Preview and Changes tabs
    $wgDefaultUserOptions['wikieditor-preview'] = 0;

    # Displays the Publish and Cancel buttons on the top right side
    $wgDefaultUserOptions['wikieditor-publish'] = 0;
    #17.01.14<-


--------------
**WikiEditor:**

You should replace at least one file of WikiEditor extension of MW 1.22 with modified file of this bundle:
- WikiEditor/modules/ext.wikiEditor.toolbar.js.

--------------
**Preferences=>Editing (your account settings of MediWiki):**

Make sure that settings in your Preferences=>Editing are valid.
>DO NOT select these:
- Show WikiTextEditor
- Start with rich editor disabled
- Open rich editor in a popup

>These may be selected:
- Use toggle to switch between wikitext and rich editor
- Remember last toggle state

====================


About browser compatibility
===

**About versions of IE:**
- IE versions 7 or below will not work with this bundle.

- With IE8, IE9, IE10, IE11 browsers, DO NOT SET browsers compatibility settings on for your wiki site, if you do have them enabled then wysiwyg will not work.

**Browser versions known to work with this bundle of WYSIWYG:**
- IE8
- IE11
- FireFox (v26.0, v27.0)
- Chrome (v.32.0.1700.76 m, v.33.0.1750.117 m)

    