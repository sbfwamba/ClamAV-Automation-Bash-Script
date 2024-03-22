# ClamAV-Automation-Bash-Script
#This is a simple bash script that can be used to automate clamav scans

#bash
#This is a bash script that is used for scanning malicious files on linux device
pdir=add_script directory #This is a parent directory
$flog=$pdir/clamscanscript.log
rdir=$pdir/Results #scan results directory path
scndir=/root/clamTest #folders to be scanned
rfls=$rdir/clamscan-results-$(date "+%Y.%m.%d.%H") #scan results files path
clamlogs=/var/log/

if [ ! -d "$rdir" ]
then 
mkdir $bdir
echo "$(date +"%b %d %H:%M:%S") The directory $bdir Created!" >> $flog 
else
echo "$(date +"%b %d %H:%M:%S") The directory $bdir exists!" >> $flog
fi

echo "$(date +"%b %d %H:%M:%S") The clamscan started" >> $flog 
clamscan -ir $scndir >> $rfls
echo "$(date +"%b %d %H:%M:%S") The clamscan ended!" >> $flog
echo "$(date +"%b %d %H:%M:%S") Adding space at the start of each output line!" >> $flog 
sed 's/^/ /' -i $rfls
echo "$(date +"%b %d %H:%M:%S") Adding space at the start of each output line done!" >> $flog
echo "$(date +"%b %d %H:%M:%S") Adding the completion of scan timestamp and hostname!" >> $flog 
sed -i "1s/^/"$(date +"%b %d %H:%M:%S")" $(hostname) ClamScan Results: \n/" $rfls
echo "$(date +"%b %d %H:%M:%S") Adding the completion of scan timestamp and hostname done!" >> $flog
echo "$(date +"%b %d %H:%M:%S") Adding the completion of scan timestamp and hostname done!" >> $flog
echo "$(date +"%b %d %H:%M:%S") Combining all the output into one message!" >> $flog
cat $rfls | tr -d '\n' >> $clamlogs
echo "$(date +"%b %d %H:%M:%S") Combining all the output into one message done!" >> $flog
echo "$(date +"%b %d %H:%M:%S") Script exiting.... I am not lazy I just want to make the work easier so that I can take more coffee. Byee! Cheers! See you soon!" >> $flog
exit
