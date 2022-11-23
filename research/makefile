research:
	pdflatex research
	biber research
	pdflatex research
	pdflatex research
	make clean
	mv research.pdf ../research.pdf

clean:
	rm -f *.aux *.bbl *.bcf *.blg *.log *.out *.run.xml *.toc *.lof *.lot *.idx *.ilg *.ind *.synctex.gz

.PHONY:
	clean report