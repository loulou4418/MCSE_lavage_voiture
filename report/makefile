# Project name is use to generate the pdf output
PRJ_NAME=MCSE_lavage_voiture

SOURCE = main
OUT_DIR = ./temp
LATEX_CMD = latex -output-format='pdf' -output-directory=$(OUT_DIR) $(SOURCE).tex

draw_src = $(shell find ./figure/ -type f -name "*.drawio.svg")
draw_target = $(draw_src:./figure/%.draw.svg=./figure/%.draw.png)
#https://unix.stackexchange.com/questions/140912/no-target-error-using-make


./$(OUT_DIR)/$(SOURCE).aux: *.tex ./texContent/* $(draw_target) makefile
	$(LATEX_CMD)
	bibtex ./$(OUT_DIR)/$(SOURCE)
	bib2gls ./$(OUT_DIR)/$(SOURCE)
#	$(LATEX_CMD)
#	$(LATEX_CMD)
	mv ./temp/main.pdf ./$(PRJ_NAME).pdf

# generate png from svg
#	Input svg file, <name>.draw.svg
#	Output png file, <name>.draw.png
./figure/%.draw.png: ./figure/%.drawio.svg
	inkscape --export-area-drawing --export-dpi=300 --export-png=$@ $<

clean:
	find . -name '*.aux' -delete

reset:
	make clean
	rm -f $(SOURCE).pdf
	rm -R -f temp
	mkdir temp
