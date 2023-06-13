        const product_images = Array.from(event.target.image.files);
        console.log(product_images)

        const imageUrls = await Promise.all(
            product_images.map(async (file) => {
                const formData = new FormData();
                formData.append('image', file);

                // const response = await axios.post('https://api.imgbb.com/1/upload?&key=c76efd57d012df5b882d44b0f8f3394f', formData);

                // const imageUplod = response.data.data.url;
                const url = 'https://api.imgbb.com/1/upload?&key=c76efd57d012df5b882d44b0f8f3394f'
                fetch(url, {
                        method: 'POST',
                        body: formData,
                    })
                        .then(res => res.json())
                        .then(data => {
                            console.log(data.data.url)
                            const product = {
                                product_name,
                                product_description,
                                product_features,
                                product_prices,
                                title: title,
                                product_images: data.data.url,
            
                            }
                            console.log(product)
                            // save doctor information to the database
                            fetch('https://project-one-server-ezazahmed16.vercel.app/products', {
                                method: 'POST',
                                headers: {
                                    'content-type': 'application/json',
                                },
                                body: JSON.stringify(product)
                            })
                                .then(res => res.json())
                                .then(result => {
                                    console.log(result);
                                    toast.success(`${product.product_name} is added successfully`);
                                    setIsLoading(false)
                                })
            
                        })
                        .catch(error => console.log(error))

            })
        );
        setProductImages(imageUrls);
        // const product = {
        //     product_name,
        //     product_description,
        //     product_features,
        //     product_prices,
        //     title: title,
        //     product_images: productImages,

        // }
        // // save doctor information to the database
        // await fetch('https://project-one-server-ezazahmed16.vercel.app/products', {
        //     method: 'POST',
        //     headers: {
        //         'content-type': 'application/json',
        //     },
        //     body: JSON.stringify(product)
        // })
        //     .then(res => res.json())
        //     .then(result => {
        //         console.log(result);
        //         toast.success(`${product.product_name} is added successfully`);
        //         setIsLoading(false)
        //     })






        // Image processing with ImageBB
        // const formData = new FormData();
        // formData.append('image', product_images)

        // const url = `https://api.imgbb.com/1/upload?&key=c76efd57d012df5b882d44b0f8f3394f`
        // fetch(url, {
        //     method: 'POST',
        //     body: formData,
        // })
        //     .then(res => res.json())
        //     .then(data => {
        //         console.log(data.data.display_url)
        //         const product = {
        //             product_name,
        //             product_description,
        //             product_features,
        //             product_prices,
        //             title: title,
        //             product_images: data.data.display_url,

        //         }
        //         console.log(product)
        //         // save doctor information to the database
        //         fetch('https://project-one-server-ezazahmed16.vercel.app/products', {
        //             method: 'POST',
        //             headers: {
        //                 'content-type': 'application/json',
        //             },
        //             body: JSON.stringify(product)
        //         })
        //             .then(res => res.json())
        //             .then(result => {
        //                 console.log(result);
        //                 toast.success(`${product.product_name} is added successfully`);
        //                 setIsLoading(false)
        //             })

        //     })
        //     .catch(error => console.log(error))