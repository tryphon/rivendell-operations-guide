namespace :dist do
  task :html do
    sh "xsltproc --xinclude --output dist/book.html /usr/share/xml/docbook/stylesheet/docbook-xsl-ns/html/docbook.xsl book.xml"
  end
  task :pdf do
    sh "xsltproc --xinclude --output dist/book.fo --stringparam paper.type A4 /usr/share/xml/docbook/stylesheet/docbook-xsl-ns/fo/docbook.xsl book.xml"
    sh "fop dist/book.fo dist/book.pdf"
  end
end
