# ǿ����bash���е�ϵͳ/bin/shĬ������dash�ģ���dash�ᵼ��echo -e��ʾʱ���һ��-e
SHELL = /bin/bash

#������
COMPILE = gcc
#������ѡ��
CFLAGS += $(INCLUDES) -Wall

#������
SHARE_LIBS +=
STATIC_LIBS +=
LIBS += $(SHARE_LIBS) $(STATIC_LIBS)

#����Ŀ��
TARGET := mydemo

#Ŀ���ļ�Ŀ¼
BUILDDIR ?= _build
TEMPDIR	?= $(BUILDDIR)/temp

#����ͷ�ļ�Ŀ¼
INCLUDES += -ImoduleMain/h -ImoduleA/h -ImoduleB/h -ImoduleC/h

#Դ�ļ�
SOURCES	+= ${wildcard moduleMain/c/*.c}
SOURCES	+= ${wildcard moduleA/c/*.c}
SOURCES	+= ${wildcard moduleB/c/*.c}
SOURCES	+= ${wildcard moduleC/c/*.c}

#�����ļ�
DEPENDS := $(patsubst %.c,$(TEMPDIR)/%.d,$(filter %.c, $(SOURCES)))
-include $(DEPENDS)

#�����ļ�
OBJECTS	:= $(patsubst %.c,$(TEMPDIR)/%.o,$(filter %.c, $(SOURCES)))

$(TEMPDIR)/%.d: %.c
	@echo "$@: $<:$(notdir $*)"
	@mkdir -pv $(@D)
	@set -e; rm -f $@; \
	$(COMPILE) -MM $(CFLAGS) $< > $@.$$$$; \
	sed 's,$(notdir $*)\.o[ :]*,$(TEMPDIR)/$*\.o $@ : ,g' < $@.$$$$ > $@; \
	rm -f $@.$$$$

$(TEMPDIR)/%.o: %.c
	@mkdir -pv $(@D)
	$(COMPILE) $(CFLAGS) -c -o $@ $<

sources:
	@echo "$(SOURCES)"

#����Ŀ¼
buildDir:
	@mkdir -pv $(BUILDDIR)
	@mkdir -pv $(TEMPDIR)

all: buildDir $(OBJECTS)
	@echo "Building for $(TARGET) ..."
	$(COMPILE) $(CFLAGS) $(OBJECTS) -o $(BUILDDIR)/$(TARGET) $(LIBS)
	@echo "********** Build Finish !!! **********"
	
clean:
	@rm -fv $(BUILDDIR) -r
