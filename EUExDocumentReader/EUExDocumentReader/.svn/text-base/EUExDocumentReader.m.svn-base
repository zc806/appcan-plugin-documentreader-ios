//
//  EUExDocumentReader.m
//  EUExDOCReader
//
//  Created by AppCan on 13-4-1.
//  Copyright (c) 2013年 AppCan. All rights reserved.
//

#import "EUExDocumentReader.h"
#import "EUtility.h"

@implementation EUExDocumentReader

@synthesize docPath;

- (id)initWithBrwView:(EBrowserView *)eInBrwView{
    
    if (self=[super initWithBrwView:eInBrwView]) {
    
    }
    return self;
}

#pragma mark - QLPreviewController DataSource 

- (NSInteger)numberOfPreviewItemsInPreviewController:(QLPreviewController *)controller 
{
    return 1;
}

- (id <QLPreviewItem>)previewController:(QLPreviewController *)controller previewItemAtIndex:(NSInteger)index
{
    NSString *path = self.docPath;
    NSURL *url = [NSURL fileURLWithPath:path];
    return url;
}

#pragma mark - QLPreviewController Delegate 

-(void)previewControllerDidDismiss:(QLPreviewController *)controller
{
    if (qlPreViewController) {
        [qlPreViewController release];
        qlPreViewController = nil;
    }
    if (self.docPath) {
        self.docPath = nil;
    }
}

#pragma mark - openDocumentReader

- (void)openDocumentReader:(NSMutableArray *)inArguments
{
    NSString *filePath = nil;
    if (inArguments != nil && [inArguments count] == 1) {
        filePath = [self absPath:[inArguments objectAtIndex:0]];
    }else {
        return;
    }
    self.docPath = filePath;
    if (!qlPreViewController) {
        qlPreViewController = [[QLPreviewController alloc] init];
    }
    qlPreViewController.dataSource = self; 
    qlPreViewController.delegate = self;
    [EUtility brwView:meBrwView presentModalViewController:qlPreViewController animated:YES];
}

#pragma mark - 进入插件界面退出后，点击“关闭”会调

- (void)close:(NSMutableArray *)inArguments
{
    if (qlPreViewController) {
        [qlPreViewController release];
        qlPreViewController = nil;
    }
    if (self.docPath) {
        self.docPath = nil;
    }
}

#pragma mark - 进入插件界面退出后，点击“返回”会调

- (void)clean
{
    if (qlPreViewController) {
        [qlPreViewController release];
        qlPreViewController = nil;
    }
    if (self.docPath) {
        self.docPath = nil;
    }
    [super clean];
}

- (void)dealloc
{
    if (qlPreViewController) {
        [qlPreViewController release];
        qlPreViewController = nil;
    }
    if (self.docPath) {
        self.docPath = nil;
    }
    [super dealloc];
}


@end

