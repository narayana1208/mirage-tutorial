all: crunch fat # vbd 

clean:
	mir-build -clean
	$(RM) vbd.img fat.img crunch.img filesystem_static.ml myocamlbuild.ml

.PHONY: all clean

# targets
crunch: crunch.bin
	./_build/unix-socket/crunch.bin

vbd: vbd.bin ## XXX broken
	./_build/unix-socket/vbd.bin -vbd static:vbd.img # ??? -kv_ro static:dummy

fat: fat.bin
	./_build/unix-socket/fat.bin -vbd dummy:fat.img -fat_kv_ro static:dummy

fat_lowlevel: fat_lowlevel.bin
	./_build/unix-socket/fat_lowlevel.bin -vbd dummy:fat.img

# exec targets
crunch.bin: crunch.mir kv_ro.ml crunch.img
	mir-build unix-socket/crunch.bin

vbd.bin: vbd.mir kv_ro.ml vbd.img
	mir-build unix-socket/vbd.bin

fat.bin: fat.ml fat.img
	mir-build unix-socket/fat.bin

fat_lowlevel.bin: fat_lowlevel.ml fat.img
	mir-build unix-socket/fat_lowlevel.bin

# disk images
vbd.img: rootdir
	mir-fs-create rootdir static
	mv static vbd.img

fat.img: rootdir
	mir-fat-create rootdir fat.img

crunch.img: rootdir filesystem_static.ml
	touch crunch.img
filesystem_static.ml: rootdir
	mir-crunch -name "static" rootdir > filesystem_static.ml

