#
# (C) Copyright 2009
# Texas Instruments, <www.ti.com>
#
# (C) Copyright 2000, 2001, 2002
# Wolfgang Denk, DENX Software Engineering, wd@denx.de.
#
# See file CREDITS for list of people who contributed to this
# project.
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# version 2 as published by the Free Software Foundation.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston,
# MA 02111-1307 USA
#

include $(TOPDIR)/config.mk

LIB	= lib$(BOARD).a

OBJS	:= cosmopolitan.o mem.o syslib.o sys_info.o clock.o mmc.o spi.o cosmo_muic.o gpio.o ifx.o charging_ic.o \
	   cosmo_dispc.o cosmo_dsi.o lge_nvdata_emmc.o sparse.o omap4.o lglogo.o web_download.o
SOBJS	:= lowlevel_init.o

$(LIB):	$(OBJS) $(SOBJS)
	$(AR) crv $@ $^

lglogo.rle: ../p2/lglogo.rle
	@rm -f lglogo.o
	ln -s ../p2/lglogo.rle lglogo.rle

web_download.rle: ../p2/web_download.rle
	@rm -f web_download.o
	ln -s ../p2/web_download.rle web_download.rle

web_download_eng.rle: ../p2/web_download_eng.rle
	@rm -f web_download_eng.o
	ln -s ../p2/web_download_eng.rle web_download_eng.rle

lglogo.o: lglogo.rle
	$(OBJCOPY) -I binary -O elf32-littlearm -B arm --redefine-sym _binary_$(patsubst %.o,%_rle_start,$@)=$(patsubst %.o,%,$@) $(patsubst %.o,%.rle,$@) $@

web_download.o: web_download.rle
	$(OBJCOPY) -I binary -O elf32-littlearm -B arm --redefine-sym _binary_$(patsubst %.o,%_rle_start,$@)=$(patsubst %.o,%,$@) $(patsubst %.o,%.rle,$@) $@

web_download_eng.o: web_download_eng.rle
	$(OBJCOPY) -I binary -O elf32-littlearm -B arm --redefine-sym _binary_$(patsubst %.o,%_rle_start,$@)=$(patsubst %.o,%,$@) $(patsubst %.o,%.rle,$@) $@

clean:
	rm -f $(SOBJS) $(OBJS)

distclean:	clean
	rm -f $(LIB) core *.bak .depend
	rm -f lglogo.rle web_dowload.rle web_download_eng.rle

#########################################################################

.depend:	Makefile $(SOBJS:.o=.S) $(OBJS:.o=.c)
		$(CC) -M $(CPPFLAGS) $(SOBJS:.o=.S) $(OBJS:.o=.c) > $@

-include .depend

#########################################################################
