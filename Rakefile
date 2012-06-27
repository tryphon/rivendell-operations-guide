namespace :dist do
  task :html do
    sh "xsltproc --xinclude --output dist/book.html /usr/share/xml/docbook/stylesheet/docbook-xsl-ns/html/docbook.xsl book.xml"
  end
  task :pdf do
    sh "xsltproc --xinclude --output dist/book.fo --stringparam paper.type A4 /usr/share/xml/docbook/stylesheet/docbook-xsl-ns/fo/docbook.xsl book.xml"
    sh "fop dist/book.fo dist/book.pdf"
  end
end

class Release

  attr_accessor :public_server, :public_directory

  def initialize
    @public_server="www.tryphon.priv"
    @public_directory="/var/www/tryphon.eu/download/rivendell/rog"
  end

  def release_name
    @release_name ||= Time.now.strftime("%Y%m%d-%H%M") # 20120627-1157
  end
  
  def publish(*formats)
    Array(formats).flatten.each do |format|
      public_file="rog-#{release_name}.#{format}"
      sh "scp dist/book.#{format} #{public_server}:#{public_directory}/#{public_file}"
      sh "ssh #{public_server} \"cd #{public_directory}; ln -fs #{public_file} latest.#{format}\""
    end
  end

end

task :release => ["dist:html","dist:pdf"] do
  Release.new.publish(:html, :pdf)
end
