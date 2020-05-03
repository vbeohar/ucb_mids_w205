default: slides README.md

weeks = $(wildcard *-*)

slides:
	@for week in $(weeks); do \
	  $(MAKE) -C $$week; \
	done
	$(MAKE) -C tutorials

README.md: docs/README.md
	@echo "---" $@ "---"
	@cp docs/README.md .

docs/README.md:
	$(MAKE) -C docs

pdfs:
	@for week in $(weeks); do \
	  $(MAKE) -C $$week $@; \
	done
	$(MAKE) -C tutorials $@

clean:
	@for week in $(weeks); do \
	  $(MAKE) -C $$week $@; \
	done
	$(MAKE) -C docs $@
	$(MAKE) -C tutorials $@

realclean: clean
	rm -f README.md
