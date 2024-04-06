# OREmining

ore \
    --rpc https://api.mainnet-beta.solana.com \
    --keypair ~/.config/solana/id.json \
    --priority-fee 1 \
    mine \
    --threads 4#!/usr/bin/env bash   

# Set environment variable to enable GPU mining
export ORE_GPU=true

export PF=100000
export SOLANA_RPC="https://api.mainnet-beta.solana.com"
start-ore-id1 () {
  ore --priority-fee $PF --rpc "$SOLANA_RPC" --keypair ~/.config/solana/id.json mine --threads 40 &
}

start-ore-id2 () {
  ore --priority-fee $PF --rpc "$SOLANA_RPC" --keypair ~/.config/solana/id2.json mine --threads 40 &
}

start-ore-id3 () {
  ore --priority-fee $PF --rpc "$SOLANA_RPC" --keypair ~/.config/solana/id3.json mine --threads 40 &
}

start-ore-id4 () {
  ore --priority-fee $PF --rpc "$SOLANA_RPC" --keypair ~/.config/solana/id4.json mine --threads 40 &
}

start-ore-id5 () {
  ore --priority-fee $PF --rpc "$SOLANA_RPC" --keypair ~/.config/solana/id5.json mine --threads 40 &
}

429_count=0

while true; do
start-ore-id || ((429_count++))
  start-ore-id2 || ((429_count++))
  start-ore-id3 || ((429_count++))
  start-ore-id4 || ((429_count++))
  start-ore-id5 || ((429_count++))

  # Sleep for 5 seconds, multiplied by the number of times we've encountered 429 errors
sleep $((5 * 429_count))
done
