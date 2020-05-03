
slides = $(wildcard *-*.md)
default: $(slides:.md=.html)
pdfs: $(slides:.md=.pdf)

run_pandoc := docker run --rm -t \
	-v `pwd`:/source \
	-v `python -c 'import os, sys; print(os.path.realpath("images"))'`:/source/images \
	-v `python -c 'import os, sys; print(os.path.realpath("reveal.js"))'`:/source/reveal.js \
	--user $(shell id -u):$(shell id -g) \
	midsw205/pandoc:2.0.7

run_decktape := docker run --rm -t \
	-v `pwd`:/slides \
	-v `python -c 'import os, sys; print(os.path.realpath("images"))'`:/slides/images \
	-v `python -c 'import os, sys; print(os.path.realpath("reveal.js"))'`:/slides/reveal.js \
	astefanutti/decktape:2.8.3 

%.html : %.md
	@echo "---" $@ "---"
	$(run_pandoc) $< -o $@ -s -t revealjs --template=/templates/mids-revealjs-template.html --section-divs --mathjax -V theme=mids -V transition=linear

%-videos.html : %-videos.md
	@echo "---" $@ "(with hosted links)---"
	$(eval hosted_revealjs_url := "http://people.ischool.berkeley.edu/~mark.mims/course-development/2017-mids-w205/templates/reveal.js/")
	$(run_pandoc) $< -o $@ -s -t revealjs --template=/templates/mids-revealjs-template.html --section-divs -V theme=mids -V transition=linear -V revealjs-url=$(hosted_revealjs_url)

%.svg : %.dot
	@echo "---" $@ "---"
	dot -T svg $< -o $@ 

%.pdf : %.html
	@echo "---" $@ "---"
	$(run_decktape) -s '1920x1080' $< $@

clean:
	rm -f *.html
	rm -f *.pdf

clobber: clean

