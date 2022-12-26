# Билди в Overleaf
research:
	xelatex research
	#bibtex research
	xelatex research
#	xelatex research
	make clean
	mv research.pdf ../research.pdf

clean:
	rm -f *.aux *.bbl *.bcf *.blg *.log *.out *.run.xml *.toc *.lof *.lot *.idx *.ilg *.ind *.synctex.gz

.PHONY:
	clean report