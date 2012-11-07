.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt


"locallang-XML" (llXML) files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The locallang-XML files contain default labels, possibly inline
translations and in addition a lot of meta data used in the
translation tool (extension “llxmltranslate”).

Performance is great with the XML files. This is because the content
of the XML file is cached based on the modification time on the xml
file.

"locallang-XML" files store the translations of a single language in
external files by default. The main reason for using external files
for locallang-XML should be distribution considerations:

- Typically installations need only English and 1-2 other backend
  languages, not all 40+!

- It allows translators to work on translations independent of extension
  authors.

- Splitting translations means we can better defend storing meta data
  for translators.

The format of locallang-XML files can look like this example (shows
inline translation of danish)::

   <T3locallang>
       <meta type="array">
           <description>Standard Module labels for Extension Development Evaluator</description>
           <type>module</type>
           <csh_table/>
           <labelContext type="array"/>
       </meta>
       <data type="array">
           <languageKey index="default" type="array">
               <label index="mlang_tabs_tab">ExtDevEval</label>
               <label index="mlang_labels_tabdescr">The Extension Development Evaluator tool.</label>
           </languageKey>
           <languageKey index="dk" type="array">
               <label index="mlang_tabs_tab">ExtDevEval</label>
               <label index="mlang_labels_tabdescr">Evalueringsværktøj til udvikling af extensions.</label>
           </languageKey>
   ....
       </data>
       <orig_hash type="array">
           <languageKey index="dk" type="array">
               <label index="mlang_tabs_tab" type="integer">114927868</label>
               <label index="mlang_labels_tabdescr" type="integer">187879914</label>
           </languageKey>
       </orig_hash>
   </T3locallang>

You can refer to `"TYPO3 Core API" for details about the XML format
<#%3CT3locallang%3E%7Coutline>`_ .


Converting to llXML from locallang.php
""""""""""""""""""""""""""""""""""""""

If you have locallang.php files in your extensions, please consider to
convert them to llXML. This can be done with the extension
“extdeveval” which contains a tool for that. After conversion there is
another tool which will separate translations out into the language
pack directories. This is of course also highly recommended so the
remaining main llXML file contains only default labels!

