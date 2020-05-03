default: README.md index.html syllabus.pdf instructor-notes.pdf 

run_pandoc := docker run --rm -t \
	-v `pwd`:/source \
	midsw205/pandoc:2.0.7

%.pdf: %.md
	@echo "---" $@ "---"
	@$(run_pandoc) $< -o $@ --toc -s 

syllabus.md: ../templates/README-template.md ../templates/README-template-footer.md $(wildcard ../*-*/README.md)
	@echo "---" $@ "---"
	@cat ../templates/README-template.md \
		../templates/README-template-section-1.md \
		$(wildcard ../01-*)/README.md \
		$(wildcard ../02-*)/README.md \
		$(wildcard ../03-*)/README.md \
		../templates/README-template-section-2.md \
		$(wildcard ../04-*)/README.md \
		$(wildcard ../05-*)/README.md \
		$(wildcard ../06-*)/README.md \
		$(wildcard ../07-*)/README.md \
		$(wildcard ../08-*)/README.md \
		../templates/README-template-section-3.md \
		$(wildcard ../09-*)/README.md \
		$(wildcard ../10-*)/README.md \
		$(wildcard ../11-*)/README.md \
		$(wildcard ../12-*)/README.md \
		../templates/README-template-section-4.md \
		$(wildcard ../13-*)/README.md \
		$(wildcard ../14-*)/README.md \
		../templates/README-template-footer.md > $@

title.md: metadata.yml
	@echo "---" $@ "---"
	@$(run_pandoc) $< -o $@ --template=title-template.md

README.md: title.md syllabus.md
	@echo "---" $@ "---"
	@cat $^ > $@

index.html: metadata.yml syllabus.md
	@echo "---" $@ "---"
	@$(run_pandoc) $^ -o $@ -s

syllabus.pdf: metadata.yml syllabus.md
	@echo "---" $@ "---"
	@$(run_pandoc) $^ -o $@ -s

clean:
	rm -f instructor-notes.pdf
	rm -f syllabus*
	rm -f README.md
	rm -f title.md

realclean: clean
	rm -f index.html
