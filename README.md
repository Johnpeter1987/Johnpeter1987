import glob
import re
import os

tit = input("Enter the title:")
auth = input("Enter the Author:")
dat =  input("Enter the Date:")
bookisbn = input("Enter the Book ISBN:")
booksrcisbn = input("Enter the pgsrcisbn :")
bookdoi = input("Enter the doi :")
bisbn1 = input("Enter the ISBN1 :")
bisbn2 = input("Enter the ISBN2 :")
bisbn3 = input("Enter the ISBN3 :")
pub = input("Enter the Publisher :")
rig = input("Enter the Rights :")
bcomp = input("Enter the Book Complexity (Simple\Medium\Complex) :")
Direc = input("Enter the path:")

path = Direc+"\**"

f = open("package.txt", "w+")
for file in glob.iglob(path, recursive=True):
        f.write(file)
        f.write("\n")
f.close()

r = open("package.txt", "r+")
p = open("package1.txt", "w+")

for splines2 in r:
        if '.jpg' in splines2:
                i = splines2
                res = i.rpartition("ops")
                res1 = res[2]
                res4 = i.rpartition("images\\")
                res5 = res4[2]
                res6 = res5.rpartition(".jpg")
                res7 = res6[0]
                
                x = res7.isnumeric()
                if x is True:
                        res2 = """<item id="cover-image" href="{}" media-type="image/jpeg" properties="cover-image"/>""" + "\n"
                        res3 = res2.format(res1)
                        p.write(res3)
                else:
                        res2 = """<item id="{}" href="{}" media-type="image/jpeg"/>""" + "\n"
                        res3 = res2.format(res7, res1)
                        p.write(res3)
        
        if '.png' in splines2:
                pi = splines2
                pres = pi.rpartition("ops")
                pres1 = pres[2]
                pres4 = pi.rpartition("images\\")
                pres5 = pres4[2]
                pres6 = pres5.rpartition(".png")
                pres7 = pres6[0]
                pres2 = """<item id="{}" href="{}" media-type="image/png"/>""" + "\n"
                pres3 = pres2.format(pres7, pres1)
                p.write(pres3)
 
        # if '.js' in splines2:
        #         num = 1
        #         j = splines2
        #         scri = j.rpartition("ops")
        #         scri1 = scri[2]
        #         scri2 = """<item id="jid" href="{}" media-type="application/x-javascript"/>""" + "\n"
        #         scri3 = scri2.format(scri1)
        #         p.write(scri3)
        
        if '.css' in splines2:
                c = splines2
                cs = c.rpartition("ops")
                cs1 = cs[2]
                cs2 = """<item id="style" href="{}" media-type="text/css"/>""" + "\n"
                cs3 = cs2.format(cs1)
                p.write(cs3)
        
        if '.xhtml' in splines2:
                h = splines2
                ht = h.rpartition("ops")
                ht1 = ht[2]
                ht4 = h.rpartition("xhtml\\")
                ht5 = ht4[2]
                ht6 = ht5.rpartition(".xhtml")
                ht7 = ht6[0]
                if ht7 == "nav":
                        ht2 = """<item id="{}" properties="nav" href="{}" media-type="application/xhtml+xml"/>""" + "\n"
                        ht3 = ht2.format(ht7, ht1)
                        p.write(ht3)
                else:
                        ht2 = """<item id="{}" href="{}" media-type="application/xhtml+xml"/>""" + "\n"
                        ht3 = ht2.format(ht7, ht1)
                        p.write(ht3)
p.close()
r.close()

fp = open("package1.txt", "r+")
fo = open("package.opf", "w+")

fo.writelines("<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n")
fo.writelines("<package version=\"3.0\" xmlns=\"http://www.idpf.org/2007/opf\" unique-identifier=\"BookID\" xml:lang=\"en\">\n")
fo.writelines("<metadata xmlns:dc=\"http://purl.org/dc/elements/1.1/\" xmlns:opf=\"http://www.idpf.org/2007/opf\">\n")
fo.writelines("<dc:title>"+tit+"</dc:title>\n")
fo.writelines("<dc:creator id=\"aut1\">"+auth+"</dc:creator>\n")
fo.writelines("<dc:format>application/ePub</dc:format>\n")
fo.writelines("<dc:date>"+dat+"</dc:date>\n")
fo.writelines("<dc:identifier id=\"BookID\">"+bookisbn+"</dc:identifier>\n")
fo.writelines("<dc:language>en</dc:language>\n")
fo.writelines("<dc:source id=\"pgsrc\">"+booksrcisbn+"</dc:source>\n")
fo.writelines("<dc:identifier>urn:doi:"+bookdoi+"</dc:identifier>\n")
fo.writelines("<dc:relation>"+bisbn1+"</dc:relation>\n")
fo.writelines("<dc:relation>"+bisbn2+"</dc:relation>\n")
fo.writelines("<dc:relation>"+bisbn3+"</dc:relation>\n")
fo.writelines("<dc:publisher>"+pub+"</dc:publisher>\n")
fo.writelines("<dc:rights>"+rig+"</dc:rights>\n")
fo.writelines("<dc:description>This new edition provides a practical view of pollution and its impact on the natural environment. Driven by the hope of a sustainable future, it stresses the importance of environmental law and resource sustainability, and offers a wealth of information based on real-world observations and expert experience.</dc:description>\n")

fo.writelines("<meta refines=\"#aut1\" property=\"role\" scheme=\"marc:relators\">aut</meta>\n")
fo.writelines("<meta refines=\"#pgsrc\" property=\"source-of\">pagination</meta>\n")
fo.writelines("<meta property=\"dcterms:modified\">"+dat+"T00:00:00Z</meta>\n")
fo.writelines("<meta property=\"schema:accessMode\">textual</meta>\n")
fo.writelines("<meta property=\"schema:accessMode\">visual</meta>\n")
fo.writelines("<meta property=\"schema:accessModeSufficient\">textual</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityFeature\">index</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityFeature\">readingOrder</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityFeature\">structuralNavigation</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityFeature\">tableOfContents</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityFeature\">printPageNumbers</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityFeature\">MathML</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityHazard\">none</meta>\n")
fo.writelines("<meta property=\"schema:accessibilityFeature\">displayTransformability</meta>\n")
fo.writelines("<meta property=\"schema:accessibilitySummary\">"+tit+" is a "+ bcomp +" book with figures, tables, lists, end notes, MathML and formatting defined with structural markup. This book contains accessibility features such as a table of content, landmark, reading order, structural navigation, index, semantic structure, print page fidelity, in-text navigation links, and backlinks returning to the first in-text citation. Linked DOIs are provided, but are not uniquely identified.</meta>\n")
fo.writelines("<meta name=\"cover\" content=\"cover-image\"/>\n")
fo.writelines("<meta name=\"keywords\" content=\"\"/>\n")
fo.writelines("</metadata>\n<manifest>")

for fplines in fp:
        ftxt = fplines
        ftxt1 = ftxt.replace("\n", "")
        ftxt2 = ftxt1.replace("<item", "\n<item")
        ftxt3 =  ftxt2.replace("href=\"\\images\\", "href=\"images/")
        ftxt4 =  ftxt3.replace("href=\"\\xhtml\\", "href=\"xhtml/")
        ftxt5 =  ftxt4.replace("href=\"\\styles\\", "href=\"styles/")
        fo.writelines(ftxt5)
        

fo.writelines("\n</manifest>\n")
fo.writelines("<spine xmlns=\"http://www.idpf.org/2007/opf\">\n")

fr = open("package.txt", "r+")

for fplines1 in fr:
        if '.xhtml' in fplines1:
                fh = fplines1
                fht1 = fh.rpartition("xhtml\\")
                fht2 = fht1[2]
                fht3 = fht2.rpartition(".xhtml")
                fht4 = fht3[0]
                if fht4 == "nav":
                        pass
                else:
                        fht5 = """<itemref idref=\"{}\"/>""" + "\n"
                        fht6 = fht5.format(fht4)
                        fo.write(fht6)
fo.write("</spine>\n</package>")                
fr.close()

fp.close()
fo.close()
