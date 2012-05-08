#------------------------------------------------------------------------------
# <copyright file="makefile" company="Atheros">
#    Copyright (c) 2008-2012 Qualcomm Atheros, Inc.  All Rights Reserved.
# 
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License version 2 as
# published by the Free Software Foundation;
#
# Software distributed under the License is distributed on an "AS
# IS" basis, WITHOUT WARRANTY OF ANY KIND, either express or
# implied. See the License for the specific language governing
# rights and limitations under the License.
# </copyright>
# 
# <summary>
# 	Wifi driver for AR6002
# </summary>
#
#------------------------------------------------------------------------------
#==============================================================================
# Author(s): ="Atheros"
#==============================================================================

#USE_GLIB=1

ifdef V210	
V210_DIR=/tftpboot/ubuntu-taiwan
endif

ifdef V210	
CC=		$(ATH_CROSS_COMPILE_TYPE)gcc
LD=		$(ATH_CROSS_COMPILE_TYPE)ld
else
CC=		$(ATH_CROSSS_COMPILE_TYPE)gcc
LD=		$(ATH_CROSSS_COMPILE_TYPE)ld
endif
SOURCES=abtfilt_main.c \
		abtfilt_wlan.c \
		abtfilt_core.c \
		abtfilt_utils.c \
		btfilter_action.c\
		btfilter_core.c
	
INCLUDES=	-I../../../include \
		-I../../../os/linux/include \
		-I../../../../include \
		-I../../../ \
		-I$(V210_DIR)/usr/include/dbus-1.0/ \
		-I$(V210_DIR)/usr/lib/dbus-1.0/include \
		-I$(V210_DIR)/usr/include/bluetooth \
			
CFLAGS=		-Wall -g -DABF_DEBUG
#LIBS= 		-ldbus-1 -lpthread -lbtfilt -lrt -lbluetooth
LIBS= 		-ldbus-1 -lpthread -lrt -lbluetooth


ifdef USE_GLIB	
SOURCES += abtfilt_bluez_dbus_glib.c

LIBS += -lgobject-2.0 -lglib-2.0 -ldbus-glib-1

INCLUDES += -I/usr/include/glib-2.0     \
			-I/usr/lib/glib-2.0/include \

OBJECTS=	$(SOURCES:.c=.o)			

else	
SOURCES += abtfilt_bluez_dbus.c

OBJECTS=	$(SOURCES:.c=.o)
endif



#LDFLAGS=	-L$(WORKAREA)/host/btfilter
#copy libbluetooth.so from /tftpboot/ubuntu-taiwan/usr/lib to /tftpboot/ubuntu-taiwan/lib [for V210]
ifdef V210	
LDFLAGS=	-L/tftpboot/ubuntu-taiwan/lib
endif
FILTERAPP=	abtfilt

all: $(OBJECTS)
	$(CC) -o $(FILTERAPP) $(OBJECTS) $(LDFLAGS) $(LIBS)

.c.o:
	$(CC) -c $(CFLAGS) $(INCLUDES) $< -o $@

clean:
	rm -f $(FILTERAPP) $(OBJECTS)
