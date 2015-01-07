
# This Makefile is for use by the hom Release Manager.
#
# requirements: Oort (http://code.google.com/p/owltools/wiki/OortIntro)
#
# To make a release, type 'make release' in this directory

OBO = http://purl.obolibrary.org/obo

initial-build: hom.obo
build: hom.obo minidiff
release: hom.obo diff

# all release files are derived from the editors version.
# we use the default Oort setup (hermit as reasoner)
hom.obo: hom-edit.owl
	ontology-release-runner $< --allow-overwrite --asserted --simple

# ----------------------------------------
# Imports
# ----------------------------------------
all_imports: imports/go_import.owl imports/pato_import.owl

imports/%_import.owl: hom-edit.owl
	owltools $< $(OBO)/$*.owl --add-imports-from-supports --extract-module -s $(OBO)/$*.owl -c --extract-mingraph  --set-ontology-id $(OBO)/go/extensions/$@ -o $@

# ----------------------------------------
# Diffs
# ----------------------------------------

# 
diff: hom.obo
	cd diffs && touch hom-diff && rm hom-*diff* && make

# Minidiff: intra-release differences
minidiff: hom.obo
	cd diffs  && touch hom-diff && rm hom-*diff* && make TGTS='html txt' SRC=../hom.obo && mail -s hom-diffs RELEASE-MANAGER@FOO.BAR < hom-combined-diff.txt

