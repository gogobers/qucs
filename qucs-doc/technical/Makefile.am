## Process this file with automake to produce Makefile.in
# 
# technical/Makefile.am
#
# Automake input file.
#
# Copyright (C) 2003, 2004, 2005, 2006, 2007 Stefan Jahn <stefan@lkcc.org>
#
# This is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2, or (at your option)
# any later version.
# 
# This software is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# 
# You should have received a copy of the GNU General Public License
# along with this package; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street - Fifth Floor,
# Boston, MA 02110-1301, USA.  
#

EXTRA_DIST = technical.tex l2h-init.cfg $(FIGURES) $(BIBFILE) \
  $(PSFILES) $(MATHFILES) $(MATHHELPS) $(CHAPTERS)

LATEX_ARGS = -interaction=nonstopmode

MATHFILES = mszl.m mscomparezl.m radius.m stabgear.m stabmoulton.m \
  stabbashford.m stabgearex.m coplanarzl.m
MATHHELPS = zpoly.m econst.m Kapprox.m
MPSFILES = $(MATHFILES:.m=.eps)
FIGURES = differential.fig biast.fig \
  nconnect.fig sparam.fig cccs.fig vccs.fig vcvs.fig ccvs.fig acstrafo.fig    \
  actrafo.fig opamp.fig gyrator.fig msline.fig newton.fig jfet.fig dcjfet.fig \
  newtondiode.fig dcdiode.fig diode.fig spdiode.fig spjfet.fig newtonbad.fig  \
  sconnectgraph.fig sconnectloop.fig sconnectpath.fig siconnectgraph.fig      \
  siconnectpath.fig siconnectloop.fig twoportiv.fig twoportab.fig dcsgp.fig   \
  twoportss.fig twoportpp.fig twoportps.fig twoportsp.fig twoportch.fig       \
  nconnect2.fig nconnect3.fig mscorner.fig sgp.fig dcsgp_spice.fig spsgp.fig  \
  noisejfet.fig noisediode.fig noisesgp.fig tcircuit.fig bridgecircuit.fig    \
  xcircuit.fig picircuit.fig mscoupled.fig msgap.fig mosphysical.fig          \
  mostypes.fig mosfet.fig mosband.fig dcmosfet.fig spmosfet.fig msgapphys.fig \
  noisemosfet.fig mscoupledphys.fig spnfile.fig transcap.fig                  \
  feuler.fig beuler.fig trapez.fig transind.fig stiffstable.fig convprob1.fig \
  convprob2.fig convprob3.fig msvia.fig cpline.fig cpscheme.fig cpconform.fig \
  mstee.fig mstee2.fig nitrafo.fig hb_concept.fig spsgp_spice.fig fft.fig     \
  lssp.fig cpopen.fig cpshort.fig cpgap.fig cpstep.fig hbn_concept.fig        \
  coupler.fig coax.fig tline.fig vam.fig vpm.fig twisted.fig dcalgo.fig       \
  mscross.fig bondwire.fig tline4p.fig
PSFILES = MNAexample.eps NLexample.eps CYexample.eps MNAnoise1.eps \
  MNAnoise2.eps Unoise.eps MNAsingular.eps Real_c.eps Real_ec.eps  \
  Real_r.eps TLpiece.eps QuarterWavelengthFilter.eps
EPSFILES = $(FIGURES:.fig=.eps)
PSFRAGTEXS = $(FIGURES:.fig=.tex) $(MATHFILES:.m=.tex)
PDFFILES = $(FIGURES:.fig=.pdf)
FRGFILES = $(FIGURES:.fig=.frg)
PDFFIGURES = $(PSFILES:.eps=.pdf) $(MPSFILES:.eps=.pdf)
BIBFILE = $(srcdir)/literature.bib
CHAPTERS = sparameter.tex noisewaves.tex dcanalysis.tex acanalysis.tex \
  transient.tex devices.tex microstrip.tex coplanar.tex acnoise.tex    \
  hbanalysis.tex grammar-common.tex grammar-qucs.tex grammar-data.tex  \
  hbnoise.tex synthesis.tex transline.tex maths.tex lineardevices.tex


technical: technical.dvi technical.ps technical.pdf
	$(TEX2PDF) technical

html:
	@tdir="tech/"; rm -rf $$tdir && mkdir $$tdir
	L2HINIT_NAME='l2h-init.cfg' $(LATEX2HTML) -dir tech technical.tex

technical.dvi: $(EPSFILES) $(PSFILES) $(MPSFILES)

SUFFIXES = .dvi .tex .pdf .ps .eps .fig .frg .m

.tex.dvi: $(CHAPTERS) $(BIBFILE)
	$(LATEX) $(LATEX_ARGS) $<
	$(BIBTEX) $*
	$(LATEX) $(LATEX_ARGS) $<
	$(LATEX) $(LATEX_ARGS) $<

.tex.pdf: $(CHAPTERS) $(BIBFILE) $(PDFFILES) $(PDFFIGURES)
	$(PDFLATEX) $<
	$(BIBTEX) $*
	$(PDFLATEX) $<
	$(PDFLATEX) -interaction=batchmode $<

.fig.eps:
	$(FIG2DEV) -L eps $< > $@

.fig.pdf:
	$(FIG2DEV) -L pdf $< > $@

.fig.frg:
	$(FIG2DEV) -L frg $< > $@

.eps.pdf:
	$(EPSTOPDF) $< -o=$@

if USE_OCTAVE
.m.eps:
	$(OCTAVE) $<
else
.m.eps:
	@echo -n not using octave to update "$@".
	@if [ ! -f $@ ]; then \
	  echo \ creating dummy.; \
	  echo "%%BoundingBox: 0 0 138 174" > $@; \
	else \
	  echo \ leaving as is.; \
	  touch $@; \
	fi
endif

.dvi.ps:
	$(DVIPS) $< -o $@

technical.pdf: technical.ps
	$(PS2PDF) $<

# installation of documentation
docdatadir = ${prefix}/share/qucs/docs/technical
docdata_DATA = technical.pdf

CLEANFILES = *~ $(EPSFILES) *.bak *.aux *.log *.toc *.pdf *.bbl *.blg *.dvi \
  $(MPSFILES) $(PDFFIGURES) $(PDFFILES) *.brf *.out $(PSFRAGTEXS) *.orig *.rej
MAINTAINERCLEANFILES = Makefile.in
DISTCLEANFILES = *.ps *.pdf
