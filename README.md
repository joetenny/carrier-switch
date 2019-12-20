# Carrier Command Line Switch

## Installation

1. Clone the Git repo
2. Make a config file. You only need to configure MySQL acccess for read/write acces to TLIVE 

Example

<pre>
git clone [REPO NAME] carrier-switch
cd carrier-switch
cp switch.conf.dist switch.conf
vim switch.conf
</pre>

## Execution

Run the carrier switch and pass the carrier definition (a filename that exists within the "definitions" directory) and
"lock" or "unlock". Alternatively you can use "disable" or "enable" respectively.

Example

<pre>
./carrier-switch.sh fastway-au lock
</pre>

## Other files

"switch.log" keeps a history of switches.

"lock-CARRIER_DEFINITION.lock" means that CARRIER_DEFINITION is in a lock state.

## Bash Autocompletion

If you DO NOT have root access you can append the following to your ~/.bashrc file.

If you DO have root access you can save this to /etc/bash_completion.d/carrier-switch

Either way, note that you have to set the path for the carrier definitions

<pre>
_carrier_switch_opts() 
{
    local cur prev opts def_dir

    def_dir=$HOME/carrier-switch/definitions/
    cur="${COMP_WORDS[COMP_CWORD]}"

    if [[ $COMP_CWORD -eq 1 ]]; then
        opts="$( ls ${def_dir} )"
        COMPREPLY=( $(compgen -W "${opts}" -- "${cur}") )
        return 0
    fi

    if [[ $COMP_CWORD -eq 2 ]]; then
        opts="lock unlock enable disable"
        COMPREPLY=( $(compgen -W "${opts}" -- "${cur}") )
        return 0
    fi
}
complete -F _carrier_switch_opts carrier-switch.sh
</pre>
