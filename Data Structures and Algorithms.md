# backtracking algorithm
[Restore IP Addresses](https://leetcode.com/problems/restore-ip-addresses/description/)
 
    function restoreIpAddresses(s: string): string[] {
        if (s.length>12) {
          return [];
        }
        function check(left,right){
          if (left!=right&&(s[left]==="0"||Number.parseInt(s.slice(left,right+1))>255)) {
            return false;
          }
          return true;
        }
        const res: string[]=[];
        const tmp: string[]=[];
        function generator(starIndex){
          if (starIndex===s.length&&tmp.length===4) {
            res.push(tmp.slice().join("."));
            return;
          }
          for (let index = starIndex; index < starIndex+3&&tmp.length<4; index++) {
            if(!check(starIndex,index)){
              continue;
            }
            tmp.push(s.slice(starIndex,index+1));
            generator(index+1);
            tmp.pop();
          }
        }
        generator(0);
        return res;
      };

**Prune by s.length>12,index < starIndex+3,tmp.length<4.because ip has up to 12 digits and each sub-ip has up to 3 digits and consists of 4 sub-ips**.
