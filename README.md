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


	git config --global user.email "rambpandey238@gmail.com"


	git config --global user.name "TechnoStartOfficial"


	Now Initialize Repos

			
6. Final process start compiling or building the rom

Note: Should be in rom directory
		
		cd

		cd dot

		. build/envsetup.sh


		export USE_CCACHE=1 && ccache -M 50G


		lunch dot_onclite-userdebug


		make bacon

		
7. Uploading the zip files
		sftp mrtechnostart@frs.sourceforge.net

 
		cd /home/frs/project/romsfor-redmi7-y3/PixelExperience/


		put ROM_NAME.zip
		
		
DONE 

Commands for keeping screen on while build process

	screen
	byobu
	byobu-enable
