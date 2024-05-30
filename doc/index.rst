.. INTEGRATE documentation master file, created by
   sphinx-quickstart on Thu Jan 24 09:18:42 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.


INTEGRATE: Fast Probabilistic inversion of EM data using informed prior models
------------------------------------------------------------------------------
Last updated: |today|.

The primary objective of INTEGRATE is to facilitate quantitative decision-making related to the exploration and exploitation of raw materials in Denmark.

We are developing a framework (including algorithms) that enables end-users to make informed decisions based on prior knowledge about the subsurface and recorded electromagnetic (EM) data. This framework will be developed and made publicly available.

The project consists of the following steps:

Prior modeling
   Tools will be developed to quantify (through forward simulation) as much information as possible about the subsurface, such as the expected distribution of lithological layers and a model that links resistivity to lithology.
   See, for example, [MADSEN2023]_.
  
Forward modeling
   We are considering using GA-AEM [GA-AEM], simPEG [SimPEG], and AarhusInv [AarhusInv]_ as forward modeling engines.
   
Probabilistic Inversion
   An implementation of the 1D probabilistic localized inversion using the **Localized Rejection Sampler** [HANSEN2021]_ and **Machine Learning** [HANSENFINLAY2022]_.

Analysis
   We will develop tools for visual illustrations of the results, such as 1D, 2D cross-sections, 3D rendering, as well as uncertainty quantification.
   Further a more advanced tool will be developed that will allow computing and visualizing, in principle, the posterior probability of any feature of the prior model.



Source Code
===========

   The current development version is available through GitHub at
   https://github.com/cultpenguin/integrate_mockup/.

.. 
   The latest stable code can be downloaded from
   http://cultpenguin.github.io/integrate/.



License (LGPL)
==============

This library is free software; you can redistribute it and/or modify it
under the terms of the GNU Lesser General Public License as published by
the Free Software Foundation; either version 2.1 of the License, or (at
your option) any later version. This program is distributed in the hope
that it will be useful, but WITHOUT ANY WARRANTY; without even the
implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
See the GNU Lesser General Public License for more details. You should
have received a copy of the GNU Lesser General Public License along with
this program; if not, write to the Free Software Foundation, Inc., 59
Temple Place - Suite 330, Boston, MA 02111-1307, USA.

The manual
----------

.. toctree::
   :maxdepth: 3
	      
   install
   algorithms      
   format
   workflow
   notebooks
   contributions
   references
   modules


   
