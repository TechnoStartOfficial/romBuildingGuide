1. Setting Up Build Environment

	sudo su
	add-apt-repository ppa:openjdk-r/ppa
	apt-get update
	sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
	exit

2. Cloning Akhil Narang Scripts

	mkdir ~/bin
	PATH=~/bin:$PATH
	cd ~/bin
	curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
	chmod a+x ~/bin/repo
	git clone https://github.com/akhilnarang/scripts.git scripts
	cd scripts
	bash setup/android_build_env.sh
	cd

3. Downloading ROM Source Code

	mkdir ROM_NAME
	cd ROM_NAME
	git config --global user.email "you@example.com"
	git config --global user.name "Your Name"
	repo init -u git://github.com/DotOS/manifest.git -b dot11							(For this example we have taken DOT OS)
	repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags

4. Clone the Device Sources

	cd ROM_NAME
	git clone <device_tree_github_link> -b <branchname> device/xiaomi/onclite
	git clone <kernel_tree_github_link> -b <branchname> kernel/xiaomi/onclite
	git clone <vendor_tree_github_link> -b <branchname> vendor/xiaomi/onclite
	git clone <common_tree_github_link> -b <branchname> common/xiaomi/onclite   (This is not necessary if needed by device then only use)

5. Doing ROM Bringup

cd device && cd xiaomi && cd onclite
We need to modify three files
	1. AndroidProducts.mk
	2. aosp_onclite.mk
	3. aosp.dependencies
All these are taken as examples from pixel experience and will be modified according to the rom we are building
So, from if are building dot os so will modify pixel experience device tree according to dot os rom device tree

	1. AndroidProducts.mk
		Command
			nano AndroidProducts.mk
		change this to according to rom in this it's dot os
		PRODUCT_MAKEFILES := \
          $(LOCAL_DIR)/aosp_onclite.mk
		  
		PRODUCT_MAKEFILES := \
          $(LOCAL_DIR)/dot_onclite.mk
		  
		Then to save press keys from keyboard
		
		CTRL+O
		ENTER
		CTRL+X
	
	2. Dependencies File
		Command
			mv aosp.dependencies dot.dependencies
	
	3.	aosp_onclite.mk File
		Command
			mv aosp_onclite.mk dot_onclite.mk
			nano dot_onclite.mk
			
			Search this line
			$(call inherit-product, vendor/aosp/config/common_full_phone.mk)	
			and change according to rom by comapring official devices devevice_tree from github. So, after modifying
			$(call inherit-product, vendor/dot/config/common_full_phone.mk)
			
			To save do the same keyboard combo as done in AndroidProducts.mk
			
			CTRL+O
			ENTER
			CTRL+X
			
6. Final process start compiling or building the rom

Note: Should be in root directory
		
		cd
		cd dot
		. build/envsetup.sh
		export USE_CCACHE=1 && ccache -M 50G
		lunch dot_onclite-userdebug
		make bacon -jX or mka bacon -jX 				(Here X defines the number of cpu cores so choose accordingly)
		
7. Uploading the zip files
		sftp afterallafk@frs.sourceforge.net 
		cd /home/frs/project/romsfor-redmi7-y3/PixelExperience/
		put ROM_NAME.zip
		
		
DONE 

Commands for keeping screen on while build process

	screen
	byobu
	byobu-enable
