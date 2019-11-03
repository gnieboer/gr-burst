# Copyright 2011 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.
install(FILES
    burst_arq.block.yml
    burst_random_drop.block.yml
    burst_padder.block.yml
    burst_scheduler.block.yml
    burst_scheduler2.block.yml
    burst_unpacker.block.yml
    burst_packer.block.yml
    burst_framer.block.yml
    burst_slicer.block.yml
    burst_tofpdu.block.yml
    burst_deframer.block.yml
    burst_framealign.block.yml
    burst_deframer.block.yml
    burst_preamble_insert.block.yml
    burst_preamble_correlator.block.yml
    burst_randomizer.block.yml
    burst_interp_cpdu.block.yml 
	burst_correlator_filter.block.yml
	burst_length_detect.block.yml
    burst_cpdu_matlab_writer.block.yml
    #burst_synchronizer.block.yml
    #burst_synchronizer_v2.block.yml
    #burst_synchronizer_v3.block.yml
    burst_decoder.block.yml
    burst_length_detect_c.block.yml
    burst_synchronizer_v4.block.yml DESTINATION share/gnuradio/grc/blocks
)
