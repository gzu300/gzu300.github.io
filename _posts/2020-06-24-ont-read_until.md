---
title: ONT Read Until
---

Matt Loose presented his ealier work on applying real-time targeted sequencing by Read Until method on human genome at London Call a few days ago. 
Previous work on real-time target sequencing hasn't been applied to human genome due to many concerns. 
In this project they selectively sequenced genes in odd number chromosomes,  717 genes from COSMIC with NA12878 cell line by enrichment of target genes. By running the sequencing for 15 hours, 
they got ~11.46X depth. Total amount of data is about 7.5Gb. They also sequenced two genes BRCA1 and PML1 with translocation in NB4 cell line. Preliminary results can 
be spot at 3rd hour of sequencing and the precise breakpoint can be seen at 15th hour.

So I also studied the code posted on github [https://github.com/LooseLab/ru](https://github.com/LooseLab/ru).  
To record down the structure of the code, details are skipped.

```python
def main():
    client = Read_Until_Client()
    run_workflow(client, analysis_worker)

def run_workflow():
    results = []
    pool = ThreadPool(n_workers)
    client.run()
    for _ in range(n_workers):
        results.append(pool.apply_async(analysis_worker)        
    pool.close()  
    
def analysis_worker():
    while client.running():
        reads = client.get_read_chunk()
        for each_read in reads:
            res = base_call_and_compare_to_ref(each_read)
            client.decide(res)
            
def base_call_and_compare_to_ref():
    called_read = GuppyCaller()
    aligned_read = Aligner(called_read)
    read_in_target_region = compare_to_ref(aligned_read)
    
    return read_in_target_region

class Read_Until_Client:
    def run(self):
        self._process_thread = Thread(target=self._runner, name=generate_name())
        self._process_thread.start()
        
    def _runner(self):
        yield self._get_and_process_read_from_device()
        
    def reset():
        return
    def stop_receive():
        return
    def unblock():
        return
    def get_read_chunk():
        return
```
