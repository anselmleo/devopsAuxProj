# devopsAuxProj
Shell scripting

#! /usr/bin/bash
echo "Hello Anselm"

# make usernames variable
USERNAMES=$(cat ./names.csv)
echo "Here are the usernames: " $USERNAMES

#create each user and add to group developers via a loop
for USERNAME in $USERNAMES
    do
        echo "creating users..."
        ! id $USERNAME && sudo useradd $USERNAME -m -g developers
        echo "creating ssh directory...;"
        [[ ! -d /home/$USERNAME/.ssh ]] && sudo (cd /home/$USERNAME/ && mkdir .ssh)
        echo "setting up authorized keys..."
        [[ -f /home/$USERNAME/.ssh/authorized_keys ]] && sudo rm -rf /home/$USERNAME/.ssh/authorized_keys
        echo "copying authorized keys..."
        sudo cp /home/$USER/.ssh/authorized_keys /home/$USERNAME/.ssh/authorized_keys
done

#delete users
# for USERNAME in $USERNAMES
#     do
#         id $USERNAME && sudo userdel -r $USERNAME
# done
